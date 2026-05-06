# CodeCart Developer API Guide (v1.3)

**English** | [简体中文](DEVELOPER_API.zh-CN.md) | [繁體中文](DEVELOPER_API.zh-TW.md) | [日本語](DEVELOPER_API.ja.md)

## Purpose

This guide is for developers and researchers who work through API calls, scripts, multi-agent frameworks, or CI/CD pipelines rather than manually copying text in a browser.

## Core Architecture

CodeCart v1.3 functions as a crystallized external memory layer. The architecture separates the human interface from the machine-readable state:

- **Human-facing UI**: The portable HTML file.
- **Machine memory**: The exported JSON cartridge (v1.3 format).
- **Prompt builder**: Extracts only active (non-superseded) nodes to minimize token costs.
- **Model contract**: The LLM is instructed to output strictly in CodeCart DSL (`+CLAIM`, `>SUPERSEDE`, `+ANCHOR`).

## Standard API Workflow

### Step 1: Export the Cartridge
Export your current project state as a JSON file using the **Advanced Mode** in the CodeCart UI.

### Step 2: Build a Compact Context Block
Extract only relevant information to inject into your prompt. The following logic ensures you don't waste tokens on superseded nodes.

**Python Example:**

```python
import json

# Load v1.3 exported cartridge
with open('codecart_export.json', 'r', encoding='utf-8') as f:
    cart = json.load(f)

active_nodes = []
for n in cart.get('nodes', []):
    # Filter: Keep all anchors and only active claims
    if n.get('type') == 'anchor' or not n.get('isSuperseded'):
        active_nodes.append(f"[{n['id']}] {n['content']}")

context_block = "[CODECART CONTEXT]\n" + "\n".join(active_nodes)
print(context_block)
```

### Step 3: Inject into Your Model Call
Force the LLM to process the context and return updates strictly in DSL format.

```python
from openai import OpenAI

client = OpenAI()

system_prompt = (
    "You are an assistant with access to a CodeCart memory cartridge. "
    "After analysis, summarize stable updates using CodeCart DSL only. "
    "Use +CLAIM(id, 'content') for new logic and >SUPERSEDE(old, new, 'why') for updates."
)

messages = [
    {"role": "system", "content": f"{system_prompt}\n\n{context_block}"},
    {"role": "user", "content": "Review the current architecture and propose a scaling strategy."}
]

resp = client.chat.completions.create(
    model="gpt-4o",
    messages=messages
)

# The model returns raw DSL
print(resp.choices[0].message.content)
```

### Step 4: Merge Back
Paste the model's DSL output back into the CodeCart **Advanced Mode** console and click **⚡ EXECUTE** to update your visual logic tree.

## Rules for Good API Usage

1. **Token Efficiency**: Never inject "dead" (superseded) nodes into the prompt.
2. **Anchor Stability**: Use `+ANCHOR` for immutable project rules to prevent "model drift".
3. **Atomic Claims**: Ensure the LLM generates one node per discrete logical conclusion.
4. **Automated Snapshots**: Save JSON snapshots after major decision points in your pipeline.
