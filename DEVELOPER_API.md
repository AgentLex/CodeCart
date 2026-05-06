# CodeCart Developer API Guide

**English** | [简体中文](DEVELOPER_API.zh-CN.md) | [繁體中文](DEVELOPER_API.zh-TW.md) | [日本語](DEVELOPER_API.ja.md)

## Purpose
This guide is for developers using CodeCart as an external memory layer for automated scripts, multi-agent frameworks, or CI/CD pipelines.

## Core Architecture
CodeCart v1.3 separates the human interface from machine memory:
- **Machine Memory**: The exported JSON cartridge.
- **Model Contract**: Strictly outputs CodeCart DSL (`+CLAIM`, `>SUPERSEDE`, `+ANCHOR`).

## Standard API Workflow

### Step 1: Export & Load
Export the JSON from the UI. Example Python loading logic:

```python
import json

with open('codecart_export.json', 'r', encoding='utf-8') as f:
    cart = json.load(f)
