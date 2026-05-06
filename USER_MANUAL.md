# CodeCart User Manual

[简体中文](USER_MANUAL.zh-CN.md) | **English**

## What CodeCart is

CodeCart is a portable, single-file memory cartridge for long AI conversations. Instead of dragging entire noisy chat histories forward, it stores only the logic that still matters. Version 1.3 operates entirely offline and automatically adapts to your system language (supporting 9 languages natively).

## Two Ways to Use

### 1. Easy Mode (New in v1.3)
Designed for quick, manual inputs without learning any syntax.
- Type your findings or rules in the input box.
- Select the node type (`Claim` or `Anchor`).
- Click `✚ Save` to instantly add it to your canvas.

### 2. Advanced Mode (For Power Users & AI)
Designed for bulk operations and direct AI integration using the CodeCart DSL (Domain Specific Language).
- Paste AI-generated instructions.
- Execute complex logic tree updates.
- Export/Import JSON data.

## The Fastest Workflow

1. Open the CodeCart portable HTML file in any browser.
2. In **Easy Mode**, add one hard rule as an `Anchor` (e.g., project boundaries or non-negotiable requirements).
3. Click `COPY PROMPT` (in the sidebar) and paste it into your AI chat to set the output format.
4. Chat with the AI normally.
5. When the AI outputs a summary, switch to **Advanced Mode**, paste the generated DSL into the console, and click `⚡ EXECUTE`.
6. Use `🧠 COLLAPSE` if you pasted raw chat text and want CodeCart to compress it into a node.
7. Click `📋 SYNC CONTEXT` to copy all active nodes before switching to a different AI model or starting a new chat session.

## Core DSL Actions (Advanced Mode)

### 1. `+ANCHOR('...')`
Use this for laws, boundaries, and constraints that should not drift.
*Example:*
`+ANCHOR('Must remain single-file and offline-capable')`

### 2. `+CLAIM(id, '...')`
Use this for current working conclusions.
*Example:*
`+CLAIM(ui_01, 'First-time users need an easy onboarding mode')`

### 3. `>SUPERSEDE(old, new, 'why')`
Use this when a newer decision replaces an older one. The old node will be greyed out.
*Example:*
`>SUPERSEDE(ui_01, ui_02, 'Easy mode works better than forcing users to learn DSL manually')`

## Suggested Best Practices

- **Keep anchors short and stable.**
- **Keep claims atomic:** One node equals one important idea.
- **Replace, don't edit:** Use `>SUPERSEDE` to replace outdated claims instead of editing history mentally. This preserves the evolution of your logic.
- **Sync frequently:** Use `SYNC CONTEXT` to bridge memory between desktop, mobile, or different LLMs.
- **Export saves:** Download the JSON file from Advanced Mode after reaching important milestones.

## A Simple Mental Model

Raw AI chat is your noisy, chaotic notebook. CodeCart is your distilled, crystallized operating memory.
