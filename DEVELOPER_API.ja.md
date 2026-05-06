# CodeCart デベロッパー API ガイド (v1.3)

[English](DEVELOPER_API.md) | [简体中文](DEVELOPER_API.zh-CN.md) | [繁體中文](DEVELOPER_API.zh-TW.md) | **日本語**

## 目的

このガイドは、ブラウザでの手動操作ではなく、APIコール、スクリプト、マルチエージェント（Multi-agent）フレームワーク、または CI/CD パイプラインを通じて CodeCart を利用する開発者や研究者を対象としています。

## コアアーキテクチャ

CodeCart v1.3 は、結晶化された外部メモリレイヤーとして機能します。そのアーキテクチャは、人間向けのインターフェースとマシンリーダーブルな状態を分離しています。

- **人間向け UI**: ポータブルな HTML ファイル（視覚化および手動調整用）。
- **マシンメモリ**: エクスポートされた JSON カートリッジ（v1.3 形式）。
- **プロンプトビルダー**: トークンコストを最小限に抑えるため、アクティブな（上書きされていない）ノードのみを抽出します。
- **モデル契約**: LLM に対し、CodeCart DSL（`+CLAIM`, `>SUPERSEDE`, `+ANCHOR`）形式での出力を厳格に要求します。

## 標準的な API ワークフロー

### ステップ 1: カートリッジのエクスポート
CodeCart UI の **詳細モード（Advanced Mode）** を使用して、現在のプロジェクト状態を JSON ファイルとしてエクスポートします。

### ステップ 2: コンパクトなコンテキストブロックの構築
プロンプトに注入するために必要な情報のみを抽出します。以下のロジックにより、廃棄されたノードにトークンを浪費しないようにします。

**Python 実装例:**

```python
import json

# v1.3 でエクスポートされたカートリッジファイルを読み込む
with open('codecart_export.json', 'r', encoding='utf-8') as f:
    cart = json.load(f)

active_nodes = []
for n in cart.get('nodes', []):
    # フィルタリング：すべてのアンカー（Anchor）と、アクティブな結論（Claim）のみを保持
    if n.get('type') == 'anchor' or not n.get('isSuperseded'):
        active_nodes.append(f"[{n['id']}] {n['content']}")

context_block = "[CODECART CONTEXT]\n" + "\n".join(active_nodes)
print(context_block)
```

### ステップ 3: モデル呼び出しへの注入
LLM にコンテキストを処理させ、更新内容を厳格に DSL 形式で返却するように強制します。

```python
from openai import OpenAI

client = OpenAI()

system_prompt = (
    "あなたは CodeCart メモリカートリッジへのアクセス権を持つアシスタントです。"
    "分析後、安定した更新内容を CodeCart DSL のみを使用して要約してください。"
    "新しいロジックには +CLAIM(id, '内容') を、更新には >SUPERSEDE(旧ID, 新ID, '理由') を使用してください。"
)

messages = [
    {"role": "system", "content": f"{system_prompt}\n\n{context_block}"},
    {"role": "user", "content": "現在のアーキテクチャをレビューし、スケーリング戦略を提案してください。"}
]

resp = client.chat.completions.create(
    model="gpt-4o",
    messages=messages
)

# モデルは生の DSL テキストを返します
print(resp.choices[0].message.content)
```

### ステップ 4: マージ（反映）
モデルが出力した DSL テキストを CodeCart の **詳細モード** コンソールに貼り付け、**⚡ 実行（EXECUTE）** をクリックして、視覚的なロジックツリーを更新します。

## 効果的な API 利用のガイドライン

1. **トークンの効率化**: 「デッド」ノード（置換済み/非アクティブ）をプロンプトに注入しないでください。
2. **アンカーの安定性**: 変更不可のプロジェクトルールには `+ANCHOR` を使用し、「モデルのドリフト（脱線）」を防ぎます。
3. **アトミックな結論**: LLM が1つの論理的結論に対して1つの独立したノードを生成するように調整してください。
4. **自動スナップショット**: パイプラインの重要な意思決定ポイントで、スクリプトを使用して JSON スナップショットを自動保存することを推奨します。
