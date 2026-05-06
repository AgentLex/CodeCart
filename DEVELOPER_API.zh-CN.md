# CodeCart 开发者 API 接入指南 (v1.3)

[English](DEVELOPER_API.md) | **简体中文** | [繁體中文](DEVELOPER_API.zh-TW.md) | [日本語](DEVELOPER_API.ja.md)

## 目的

本指南面向通过 API 调用、脚本、多智能体（Multi-agent）框架或 CI/CD 流水线使用 CodeCart 的开发者与研究员，旨在实现逻辑记忆的自动化管理。

## 核心架构

CodeCart v1.3 作为一个结晶化的外部记忆层，其架构将人类交互界面与机器可读的状态分离：

- **人类交互 UI**：便携式 HTML 文件（用于可视化和手动微调）。
- **机器记忆**：导出的 JSON 卡带（v1.3 格式）。
- **上下文构建器**：仅提取活跃（未被替代）的节点，以最小化 Token 成本。
- **模型契约**：指令要求 LLM 严格按照 CodeCart DSL（`+CLAIM`, `>SUPERSEDE`, `+ANCHOR`）输出。

## 标准 API 工作流

### 第 1 步：导出卡带
在 CodeCart UI 的**高级模式**中，将当前项目状态导出为 JSON 文件。

### 第 2 步：构建精简上下文块
仅提取相关信息注入提示词。以下逻辑确保你不会在已废弃的节点上浪费 Token。

**Python 示例：**

```python
import json

# 加载 v1.3 导出的卡带文件
with open('codecart_export.json', 'r', encoding='utf-8') as f:
    cart = json.load(f)

active_nodes = []
for n in cart.get('nodes', []):
    # 过滤：保留所有锚点（Anchor）和仅活跃的结论（Claim）
    if n.get('type') == 'anchor' or not n.get('isSuperseded'):
        active_nodes.append(f"[{n['id']}] {n['content']}")

context_block = "[CODECART CONTEXT]\n" + "\n".join(active_nodes)
print(context_block)
```

### 第 3 步：注入模型调用
强制要求 LLM 处理上下文，并严格以 DSL 格式返回更新。

```python
from openai import OpenAI

client = OpenAI()

system_prompt = (
    "你是一个拥有 CodeCart 记忆卡带访问权限的助手。"
    "在分析后，请仅使用 CodeCart DSL 总结稳定的更新。"
    "使用 +CLAIM(id, '内容') 记录新逻辑，使用 >SUPERSEDE(旧ID, 新ID, '原因') 更新逻辑。"
)

messages = [
    {"role": "system", "content": f"{system_prompt}\n\n{context_block}"},
    {"role": "user", "content": "审查当前的架构并提出扩展策略。"}
]

resp = client.chat.completions.create(
    model="gpt-4o",
    messages=messages
)

# 模型返回原始的 DSL 文本
print(resp.choices[0].message.content)
```

### 第 4 步：合并回传
将模型输出的 DSL 文本粘贴回 CodeCart 的**高级模式**控制台，点击 **⚡ 执行**，即可完成视觉逻辑树的更新。

## 高效使用准则

1. **Token 效率**：严禁将“死亡”节点（已置灰/被替代）注入提示词。
2. **锚点稳定性**：对于不可更改的项目准则，务必使用 `+ANCHOR` 以防止“模型漂移”。
3. **原子化结论**：确保 LLM 针对每个离散的逻辑结论生成一个独立节点。
4. **自动化快照**：在流水线的重要决策点，通过脚本自动保存 JSON 快照。
