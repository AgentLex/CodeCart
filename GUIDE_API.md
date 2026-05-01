# CodeCart API Workflow Guide

## Purpose

This guide is for users who work through API calls, scripts, agents, or pipelines rather than copying text manually in a browser.

## Core idea

Use CodeCart as an external memory layer:

1. Store validated logic in CodeCart JSON.
2. Extract active nodes into a compact context block.
3. Inject that block into your API prompt.
4. Ask the model to answer with CodeCart DSL.
5. Parse the DSL and append it back into your cartridge.

## Minimal workflow

### Step 1: Export your cartridge
Save the current cartridge as JSON from the web UI.

### Step 2: Build a compact context block
Example Python:

```python
import json

with open('codecart.json', 'r', encoding='utf-8') as f:
    cart = json.load(f)

active_nodes = []
for n in cart.get('nodes', []):
    if n.get('type') == 'anchor' or not n.get('isSuperseded'):
        active_nodes.append(f"[{n['id']}] {n['content']}")

context_block = "[CODECART CONTEXT]
" + "
".join(active_nodes)
print(context_block)
```

### Step 3: Inject into your model call

```python
from openai import OpenAI

client = OpenAI()

messages = [
    {
        "role": "system",
        "content": (
            "You are working with a CodeCart memory cartridge. "
            "After analysis, summarize stable updates using CodeCart DSL only. "
            "Use +CLAIM(id, 'content') for new logic and >SUPERSEDE(old, new, 'why') for updates."
        )
    },
    {
        "role": "system",
        "content": context_block
    },
    {
        "role": "user",
        "content": "Review the current product onboarding flow and propose one improvement."
    }
]

resp = client.chat.completions.create(
    model="gpt-4o",
    messages=messages
)

print(resp.choices[0].message.content)
```

### Step 4: Parse returned DSL
At minimum, store the raw DSL text. Better: parse it into structured updates and write back into the JSON cartridge.

## Recommended architecture

- **Human-facing UI**: CodeCart HTML
- **Machine memory file**: exported JSON
- **Prompt builder**: extracts active nodes only
- **Model response contract**: DSL-only update block
- **Merger**: applies new claims or supersedes old ones

## Rules for good API usage

- Do not inject every historical node; only active ones.
- Keep anchors separate from replaceable claims.
- Treat `>SUPERSEDE` as the source of recency.
- Add your own confidence layer later if your pipeline needs it.
- Save snapshots after major decision points.

## Best use cases

- Long-running research projects
- Multi-agent collaboration
- Cross-model review workflows
- Cost-sensitive API usage where repeated context is expensive
