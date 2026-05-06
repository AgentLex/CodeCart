# CodeCart 開發者 API 接入指南 (v1.3)

[English](DEVELOPER_API.md) | [简体中文](DEVELOPER_API.zh-CN.md) | **繁體中文** | [日本語](DEVELOPER_API.ja.md)

## 目的

本指南面向透過 API 調用、腳本、多智能體（Multi-agent）框架或 CI/CD 流水線使用 CodeCart 的開發者與研究員，旨在實現邏輯記憶的自動化管理。

## 核心架構

CodeCart v1.3 作為一個結晶化的外部記憶層，其架構將人類互動界面與機器可讀的狀態分離：

- **人類互動 UI**：便攜式 HTML 檔案（用於可視化和手動微調）。
- **機器記憶**：導出的 JSON 卡帶（v1.3 格式）。
- **上下文構建器**：僅提取活躍（未被替代）的節點，以最小化 Token 成本。
- **模型契約**：指令要求 LLM 嚴格按照 CodeCart DSL（`+CLAIM`, `>SUPERSEDE`, `+ANCHOR`）輸出。

## 標準 API 工作流

### 第 1 步：導出卡帶
在 CodeCart UI 的**高級模式**中，將目前專案狀態導出為 JSON 檔案。

### 第 2 步：構建精簡上下文塊
僅提取相關資訊注入提示詞。以下邏輯確保你不會在已廢棄的節點上浪費 Token。

**Python 示例：**

```python
import json

# 載入 v1.3 導出的卡帶檔案
with open('codecart_export.json', 'r', encoding='utf-8') as f:
    cart = json.load(f)

active_nodes = []
for n in cart.get('nodes', []):
    # 過濾：保留所有錨點（Anchor）和僅活躍的結論（Claim）
    if n.get('type') == 'anchor' or not n.get('isSuperseded'):
        active_nodes.append(f"[{n['id']}] {n['content']}")

context_block = "[CODECART CONTEXT]\n" + "\n".join(active_nodes)
print(context_block)
```

### 第 3 步：注入模型調用
強制要求 LLM 處理上下文，並嚴格以 DSL 格式返回更新。

```python
from openai import OpenAI

client = OpenAI()

system_prompt = (
    "你是一個擁有 CodeCart 記憶卡帶訪問權限的助手。"
    "在分析後，請僅使用 CodeCart DSL 總結穩定的更新。"
    "使用 +CLAIM(id, '內容') 記錄新邏輯，使用 >SUPERSEDE(舊ID, 新ID, '原因') 更新邏輯。"
)

messages = [
    {"role": "system", "content": f"{system_prompt}\n\n{context_block}"},
    {"role": "user", "content": "審查目前的架構並提出擴展策略。"}
]

resp = client.chat.completions.create(
    model="gpt-4o",
    messages=messages
)

# 模型返回原始的 DSL 文本
print(resp.choices[0].message.content)
```

### 第 4 步：合併回傳
將模型輸出的 DSL 文本貼回 CodeCart 的**高級模式**控制台，點擊 **⚡ 執行**，即可完成視覺邏輯樹的更新。

## 高效使用準則

1. **Token 效率**：嚴禁將「死亡」節點（已置灰/被替代）注入提示詞。
2. **錨點穩定性**：對於不可更改的專案準則，務必使用 `+ANCHOR` 以防止「模型漂移」。
3. **原子化結論**：確保 LLM 針對每個離散的邏輯結論生成一個獨立節點。
4. **自動化快照**：在流水線的重要決策點，透過腳本自動保存 JSON 快照。
