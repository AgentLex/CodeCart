# 🐣 CodeCart Beginner's Manual / 小白快速上手手册

Welcome to **CodeCart**, your personal "Cognitive Memory Cartridge." This tool is designed to crystallize logic from chaotic AI conversations.
欢迎来到 **CodeCart**，你的私人“认知记忆卡带”。本工具旨在从混乱的 AI 对话中提炼并固化逻辑精粹。

---

## 1. Core Concept / 核心理念

### Why use it? / 为什么要用它？
In long AI chats, models often become "forgetful" or "hallucinate" as the context window fills with noise. CodeCart acts as an external hard drive for your logic:
在长期的 AI 对话中，随着上下文充满了废话，模型往往会变得“健忘”或产生“幻觉”。CodeCart 充当了你逻辑的外部硬盘：

- **Token Efficiency / 节约成本**: Condense 10,000 words into 10 key claims.
- **Token 效率**: 将万字长谈坍缩为 10 条核心结论，减少重复解释的成本。
- **Logic Sovereignty / 逻辑主权**: You decide what is true, not the AI.
- **逻辑主权**: 由你决定什么是真理，而不是任由 AI 随机发挥。
- **Cross-Platform Alignment / 跨平台对齐**: Use the same logic "Cartridge" across multiple AIs to let them discuss based on your defined facts.
- **跨平台对齐**: 在不同 AI 平台之间传递同一套逻辑卡带，实现跨平台的协同推演。

---

## 2. Interface Breakdown / 界面功能详解

### Top Bar / 顶部状态栏
- **Token Saved / Token 已节约**: Real-time feedback on how much "chat noise" you've eliminated.
- **Token 已节约**: 实时反馈你清理了多少对话噪音。
- **EN/ZH**: Toggle system language instantly.
- **EN/ZH**: 瞬时切换系统语言。
- **🌓 Theme**: Switch between Professional Dark and Lab Light modes.
- **🌓 模式**: 在专业深色和实验室浅色模式间切换。
- **Help (?)**: Quick command cheat sheet.
- **Help (?)**: 指令快速参考表。

### Sidebar / 侧边栏
- **Prompt Helper / 调教助手**: Generates a "System Instruction" for your AI to make it output CodeCart-compatible commands.
- **调教助手**: 生成一段“系统指令”发给 AI，让它乖乖按 CodeCart 的格式输出结论。
- **Sync Context / 复制上下文**: The most important button. Packs all active logic into your clipboard to "Update" the AI's mind.
- **复制上下文**: 最重要的按钮。将所有有效逻辑打包到剪贴板，用于瞬时“更新” AI 的大脑，使其接入当前进度。

### Footer Console / 底部控制台
- **+CLAIM / +结论**: Add a factual logic node. / 添加原子级的逻辑结论节点。
- **>SUPERSEDE / >替代**: Update an old node with a new one. / 用新结论替代旧结论，记录思维演化。
- **+ANCHOR / +锚点**: Set an unshakeable law/constraint. / 设置不可动摇的底线约束或物理边界。
- **+ATTACH / +附件**: Link a local file path or URL to a node. / 为节点关联本地文件路径或云端链接。
- **Execute / 执行指令**: Run the DSL commands in the input box. / 执行输入框内的 DSL 指令。
- **Smart Collapse / 智能坍缩**: Automatically refine long raw text into a node. / 自动将长文本精炼为逻辑节点。

---

## 3. The Golden Workflow / 黄金工作流

To ensure success, please follow these **4 Steps**:
为了确保操作不卡壳，请严格遵循以下 **4 个步骤**：

### Step 1: Establish Anchors / 第一步：确立锚点
Before starting, set your "Truth Boundaries." 
在开始讨论前，先设定你的“项目底线”。
1. Click **+ANCHOR**. / 点击 **+锚点**。
2. Input your hard constraints in the brackets (e.g., `+ANCHOR('必须是手持设备')`). / 在括号内输入硬约束。
3. Click **Execute / 执行指令**. / 点击 **执行指令**。

### Step 2: Educate your AI / 第二步：调教你的 AI
Make the AI understand your language.
让 AI 理解你的协作协议。
1. Click **Copy Prompt / 复制调教语** in the sidebar. / 点击侧边栏的 **复制调教语**。
2. Paste it to your AI as the first message. / 将其作为第一条消息发送给你使用的 AI。
3. The AI will now output logic nodes automatically in future chats. / 之后 AI 会自动在回复中输出逻辑指令。

### Step 3: Sync & Commit / 第三步：同步与固化
When the AI yields a great insight during discussion:
当 AI 在讨论中产生了一个绝佳见解时：
1. **If AI gives DSL**: Copy the `+CLAIM(...)` or `>SUPERSEDE(...)` back to CodeCart and **Execute**.
   **如果 AI 给了指令**: 直接把指令贴回 CodeCart 并点击 **执行**。
2. **If AI gives raw text**: Paste the paragraph into the box and click **Smart Collapse**. Assign an ID (e.g., `phy_01`).
   **如果 AI 给了长文本**: 把内容贴进输入框，点击 **智能坍缩**。为其分配一个 ID（如 `phy_01`）。

### Step 4: Cross-AI Interaction / 第四步：AI 间互动讨论
Want AI-B to review AI-A's logic?
想让 AI-B 审阅 AI-A 的方案？
1. In AI-A, get the conclusions. Commit to CodeCart. / 从 AI-A 获取结论并固化。
2. Click **Sync Context / 复制上下文**. / 点击侧边栏的 **复制上下文**。
3. Paste the context into AI-B with a prompt: "Review this logic from the cartridge." / 将背景粘贴给 AI-B 并提问：“请审阅这些卡带逻辑”。

---

## 4. Command Reference / 指令速查表

| Command / 指令 | Example / 示例 | Usage / 用途 |
| :--- | :--- | :--- |
| **+CLAIM** | `+CLAIM(id, '内容')` | **Fact**: Assign a unique ID to a logic point. <br> **结论**: 为逻辑点分配一个唯一 ID。 |
| **>SUPERSEDE** | `>SUPERSEDE(old, new, 'why')` | **Evolution**: Mark old logic as invalid and point to the new one. <br> **演化**: 废弃旧逻辑，指向并启用新结论。 |
| **+ANCHOR** | `+ANCHOR('Content')` | **Law**: Hard constraints that never decay. <br> **锚点**: 永远不会被覆盖的硬约束。 |
| **@ATTACH** | `@ATTACH('Path')` | **Asset**: Link file evidence to the node. <br> **附件**: 为节点绑定外部文件路径。 |

---

## 5. Tips / 小贴士
- **ID Strategy**: Use prefixes like `phy_` (physics), `hw_` (hardware), `quant_` (trading).
- **ID 命名策略**: 使用分类前缀（如 `phy_` 代表物理，`hw_` 代表硬件,`quant_` 代表量化）。
- **Mouse Hover**: Mouse hover to view full text, timestamp, and delete button.
- **鼠标悬停**: 鼠标移至节点可查看详情、创建时间及删除按钮。
- **Smart Collapse Tip**: Paste your long historical chats here to "catch up" old data.
- **坍缩技巧**: 将以前没用 CodeCart 时的长对话贴进来点“智能坍缩”，可以一键追回旧账。

---

## 6. Support the Lab / 捐赠与支持
- **Developed by LexXu in Shanghai. 由上海的 Lexxu 研发。**:
- **Ko-fi: [lexxu](https://ko-fi.com/lexxu) Crypto (ETH/ENS): 0xF729Db34e9733d74c992a27AA812cFF5363C82e0**

