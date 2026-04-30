# CodeCart: The Cognitive Memory Cartridge for Human-AI Collaboration
# CodeCart：人机协作认知记忆卡带

CodeCart is a portable, single-file cognitive memory cartridge designed to end "AI Memory Pollution." It collapses thousands of words into structured logic nodes using a robust DSL engine.
CodeCart 是一款专为终结“AI 记忆污染”而生的单文件认知图谱容器。它通过强大的 DSL 引擎，将万字长谈坍缩为结构化的认知节点。

---

## 🚀 快速上手指南 / Quick Start Guide

### 第一步：开启认知白板 / Step 1: Initialize
1. **🆕 New Cartridge**: Click left-bottom button to clear all nodes.
1. **🆕 新建卡带**：点击左下角按钮，抹除所有节点，开启纯净画布。
2. **⚓ Set Anchors**: In the console, enter your hard constraints.
2. **⚓ 设定锚点**：在控制台输入物理级红线。
  - *Example:* `+ANCHOR("Budget limit: $1000")` / `+ANCHOR("预算限额 1000 元")`
3. **⚡ 执行
3. **⚡ Execute

### 第二步：认知同步循环 / Step 2: The Cognitive Loop
1. **📋 Copy for AI**: Click the button to get a compressed Markdown context.
1. **📋 复制给 AI**：点击按钮，系统自动将当前逻辑状态压缩为 Markdown。
2. **💬 Chat with AI**: Paste the text to any AI (Gemini, Perplexity, Grok).
2. **💬 对话 AI**：将文本贴给任意 AI，并要求其以 DSL 格式回答。
3. **⚡ Get & Exec**: Copy the DSL commands from AI, paste back to console, and click **Execute**.
3. **⚡ 执行指令**：复制 AI 回复的 DSL 指令，贴回控制台点击“执行”，见证节点涌现。

---

## 🧠 高阶方案：安插文档与跨模型协作 / Advanced Workflows

### 方案 A：认知坍缩（安插长文档/对话） / Scenario A: Cognitive Collapse
If you have long PDF documents or 100+ chat logs, do not paste them directly to all AIs.
如果您有长篇 PDF 或上百轮聊天记录，不要直接发给所有 AI。
1. **Feeding**: Upload document to AI A (e.g., Claude/Gemini).
1. **喂料**：将文档发给 AI A。
2. **Shrinking**: Ask AI A to "Collapse the core logic into 3-5 CodeCart `+CLAIM` commands."
2. **坍缩**：要求 AI A “将核心逻辑坍缩为 3-5 条 CodeCart `+CLAIM` 指令”。
3. **Injecting**: Paste these commands into CodeCart.
3. **注入**：将指令贴入 CodeCart。这样，复杂的文档就变成了可参与讨论的结构化节点。

### 方案 B：跨模型逻辑接力 / Scenario B: Cross-Model Relay
1. **AI A (Strategist)**: Ask Perplexity to propose a solution. Execute its `+CLAIM`.
1. **AI A（战略家）**：让 Perplexity 提出方案，执行其 `+CLAIM`。
2. **AI B (Critic)**: Sync to Grok and ask: "Find logic holes in AI A's claim and optimize."
2. **AI B（批判家）**：同步上下文给 Grok 并问：“找出 AI A 的逻辑漏洞并进行优化。”
3. **Evolution**: AI B will output `>SUPERSEDE` to refine the knowledge graph.
3. **演化**：AI B 会输出 `>SUPERSEDE` 指令，看图谱如何从旧逻辑中进化。

---

## 🤖 针对 API 用户与 Agent 协议 / For API & Agent Users

If you are an API developer, inject this into your **System Prompt**:
如果您是 API 开发者，请将此段加入您的**系统提示词**：

> "You are an expert cognitive architect. Refer to the CodeCart Context. Your output MUST conclude with DSL:
> - `+CLAIM(ID, 'Statement')` for new logic.
> - `>SUPERSEDE(old_id, new_id, 'Reason')` for updates.
> - No explanations. Just the logic commit."

---

## 🌍 Portable & Offline Version / 离线便携版

CodeCart is designed with a **Zero-Dependency** architecture. You don't need a server or internet to use it.
CodeCart 采用**零依赖**架构设计，您无需服务器或互联网即可使用。

### How to use offline / 如何离线使用：
1. **Download**: Get the `index.html` from this repo or download the standalone file from the [Releases](https://github.com/AgentLex/CodeCart/releases) page.
2. **下载**：从本仓库下载 `index.html`，或从 [Releases](https://github.com/AgentLex/CodeCart/releases) 页面下载独立文件。
3. **Run**: Double-click the file to open it in any modern browser. It works via `file:///` protocol.
4. **运行**：双击文件即可在任何现代浏览器中开启，支持本地协议运行。
5. **Security**: 100% Client-side. Your cognitive data never leaves your computer.
6. **安全**：100% 客户端运行，您的认知数据绝不会离开您的电脑。

---

## 🛠 指令集参考 / DSL Syntax Reference

| Command 指令 | Effect 作用 | Example 示例 |
| :--- | :--- | :--- |
| **+CLAIM** | Add new knowledge 新增节点 | `+CLAIM(ent_01, "方案 A 可行")` |
| **>SUPERSEDE** | Refute/Update 替代旧逻辑 | `>SUPERSEDE(clm_01, clm_02, "发现漏洞")` |
| **+ANCHOR** | Hard constraint 物理红线 | `+ANCHOR("所有代码须使用 Python 3.10")` |

---

## 🌍 全球化适用 / Global Design
* **Partitioned UI**: Shades of gray distinguish sidebar, canvas, and console.
* **分区 UI**：通过不同深浅的灰色区分边栏、画布与控制台，减少视觉疲劳。
* **Micro-Precision Timeline**: Backtrack through decisions second-by-second.
* **高精度时间轴**：支持分秒级回溯，即使是连续快速操作也能精准还原。
* **Data Sovereignty**: 100% Offline. Your logic never leaves your local file.
* **数据主权**：100% 离线，您的认知逻辑永远不会离开本地文件。

---
Created by **AgentLex**. Open Source under MIT License.
