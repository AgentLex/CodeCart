# CodeCart Beginner Guide

## What CodeCart is

CodeCart is a single-file memory cartridge for long AI conversations. Instead of dragging entire chat histories forward, it stores only the logic that still matters.

## The fastest way to start

1. Open CodeCart.
2. Click `+ANCHOR` and define one hard rule, such as a project boundary or non-negotiable requirement.
3. Click `COPY PROMPT` and paste that instruction into your AI chat.
4. Ask your question normally.
5. Copy the AI-generated DSL back into CodeCart and click `EXECUTE`.
6. When the AI replies with a long paragraph instead of DSL, paste it into CodeCart and click `COLLAPSE`.
7. Click `SYNC CONTEXT` before switching to another AI or starting a new session.

## Four core actions

### 1. `+ANCHOR('...')`
Use this for laws, boundaries, and constraints that should not drift.

Example:
```text
+ANCHOR('Must remain single-file and offline-capable')
```

### 2. `+CLAIM(id, '...')`
Use this for current working conclusions.

Example:
```text
+CLAIM(ui_01, 'First-time users need an onboarding guide')
```

### 3. `>SUPERSEDE(old, new, 'why')`
Use this when a newer decision replaces an older one.

Example:
```text
>SUPERSEDE(ui_01, ui_02, 'Auto-showing the guide works better than making users find it manually')
```

### 4. `COLLAPSE`
Use this when you only have raw chat text and want CodeCart to compress it into a node quickly.

## Suggested workflow

- Keep anchors short and stable.
- Keep claims atomic: one node, one important idea.
- Replace outdated claims instead of editing history mentally.
- Sync context before switching models or devices.
- Export saves after important milestones.

## What not to put into CodeCart

- Full transcripts that nobody will read again
- Temporary wording experiments
- Repeated explanations that do not change project state
- Low-value fluff from AI replies

## A simple mental model

Raw chat is your noisy notebook. CodeCart is your distilled operating memory.
