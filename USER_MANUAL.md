# CodeCart User Manual

**English** | [简体中文](USER_MANUAL.zh-CN.md) | [繁體中文](USER_MANUAL.zh-TW.md) | [日本語](USER_MANUAL.ja.md)

## What CodeCart is

CodeCart is a portable, single-file memory cartridge for long AI conversations. Instead of dragging entire noisy chat histories forward, it stores only the logic that still matters. Version 1.3 operates entirely offline and automatically adapts to your system language (supporting 9 languages natively).

## Two Ways to Use

### 1. Easy Mode (New in v1.3)
Designed for quick, manual inputs without learning any syntax.
- Type your findings or rules in the input box.
- Select the node type (`Claim` or `Anchor`).
- Click `✚ Save` to instantly add it to your canvas.

### 2. Advanced Mode (For Power Users & AI)
Designed for bulk operations and direct AI integration using the CodeCart DSL.
- Paste AI-generated instructions.
- Execute complex logic tree updates.
- Export/Import JSON data.

## The Fastest Workflow

1. Open the CodeCart portable HTML file in any browser.
2. In **Easy Mode**, add one hard rule as an `Anchor`.
3. Click `COPY PROMPT` and paste it into your AI chat to set the format.
4. Chat normally, then paste the AI's DSL output into **Advanced Mode** and click `⚡ EXECUTE`.
5. Click `📋 SYNC CONTEXT` to copy active nodes before starting a new session.

## Core DSL Actions

- `+ANCHOR('...')`: For non-negotiable project boundaries.
- `+CLAIM(id, '...')`: For current working conclusions.
- `>SUPERSEDE(old, new, 'why')`: To evolve old logic with newer decisions.
