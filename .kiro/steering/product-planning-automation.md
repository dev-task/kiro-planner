---
inclusion: always
---

# 企画業務自動化システム - AI-DLC (AI-Driven Life Cycle)

このステアリングルールは、プロダクト企画業務の完全自動化を実現するための指針です。

## 自動化の全体フロー

### 企画業務の8ステップ（コアフロー）

1. **① 事業・課題インプット** → 2. **② 企画スコープ定義** → 3. **③ 価値・体験整理** → 4. **④ 業務洗い出し** → 5. **⑤ 業務ロジック整理** → 6. **⑥ 要件レベルへの翻訳（PRD作成）** → 7. **⑦ プロダクトバックログ作成** → 8. **⑧ PBI粒度への分解** → 9. **Notion 登録**

### その他の自動化機能

- **ソース解析** → **仕様書生成**
- **データ分析** → **改善提案**
- **フィードバック分析** → **PBI自動生成**
- **ピボット評価** → **方向性変更の検知**

## プロジェクト構造

```
.kiro/
├── steering/           # 自動化ルール・ガイドライン
├── agents/            # 専門エージェント定義
├── hooks/             # イベントトリガー設定
└── settings/
    └── mcp.json       # MCP連携設定（Notion, GitHub等）
```

## 企画業務の自動化原則

### 1. 事業・課題インプットの自動化

- ユーザーとの対話を通じて情報収集
- 事業課題の明文化
- ターゲットユーザー定義
- KGI/KPI設定
- 制約条件の整理

### 2. 企画スコープ定義の自動化

- 既存の「戦略的4階層プロダクト.md」を活用
- プロダクト4階層（Core/Why/What/How）の整理
- やる/やらないの明確化
- フェーズ分割（MVP/v1/v2）

### 3. 価値・体験整理の自動化

- UJM（User Journey Map）の自動生成
- インセプションデッキの作成
- Aha Momentの特定
- 離脱ポイントの分析

### 4. 業務洗い出しの自動化

- ユーザー業務の列挙
- 運営業務（CS・運用）の列挙
- 自動化/人対応の分類
- 通常系/例外系の分類

### 5. 業務ロジック整理の自動化

- トリガーの定義
- 主体（誰がやるか）の明確化
- 判定条件の整理
- 処理内容の詳細化
- 状態変化の定義

### 6. 要件レベルへの翻訳の自動化

- 「prd作成.md」のテンプレートに基づく自動生成
- 業務ロジック → システム要件への変換
- 機能要件・非機能要件の整理
- 優先度（MoSCoW）の自動判定

### 7. プロダクトバックログ作成の自動化

- PRDから自動的にプロダクトバックログを生成
- エピック → ユーザーストーリー → タスクの階層構造
- 見積もり（ストーリーポイント）の自動算出
- 依存関係の整理

### 8. PBI粒度への分解の自動化

- バックログアイテムをPBI粒度に分割
- 背景・受入条件・業務ルールの付与
- 開発チームへの引き渡し準備

### 9. Notion連携の自動化

- MCP経由でNotionデータベースへ自動登録
- PBIのステータス同期
- 進捗レポートの自動生成

### 10. ソース解析の自動化

- GitHubリポジトリの自動スキャン
- アーキテクチャ図の自動生成
- 技術的負債の検出と優先順位付け

### 11. データ分析の自動化

- MCP経由で分析データを取得
- KPI自動計算とトレンド分析
- 改善提案の自動生成

## ドキュメント参照

企画業務では以下のドキュメントを常に参照します：

- #[[file:prompt_sample/戦略立案フレームワーク.md]]
- #[[file:prompt_sample/戦略的4階層プロダクト.md]]
- #[[file:prompt_sample/prd作成.md]]

## 出力フォーマット

### 事業・課題インプット

- Markdown形式
- 保存先: `docs/input/{project-name}-business-input.md`

### 企画スコープ定義

- Markdown形式
- 保存先: `docs/scope/{project-name}-scope.md`

### UJM/インセプションデッキ

- Markdown形式
- 保存先: `docs/experience/{project-name}-ujm.md`

### 業務洗い出し

- Markdown形式
- 保存先: `docs/process/{project-name}-business-process.md`

### 業務ロジック整理

- Markdown形式
- 保存先: `docs/logic/{project-name}-business-logic.md`

### PRD

- Markdown形式
- 保存先: `docs/prd/{project-name}-prd.md`

### プロダクトバックログ

- Markdown形式
- 保存先: `docs/backlog/{project-name}-backlog.md`

### PBI（プロダクトバックログアイテム）

- Markdown形式: `docs/pbi/{project-name}-pbi.md`
- JSON形式（Notion API用）: `docs/pbi/{project-name}-pbi.json`

## エージェント連携

各専門エージェントが協調して企画業務を自動化します：

### 企画フローエージェント（8ステップ）

- **business-input-agent**: 事業・課題インプット
- **scope-definition-agent**: 企画スコープ定義
- **value-experience-agent**: 価値・体験整理（UJM/インセプション）
- **business-process-agent**: 業務洗い出し
- **business-logic-agent**: 業務ロジック整理
- **requirements-agent**: 要件レベルへの翻訳（PRD作成）
- **product-backlog-agent**: プロダクトバックログ作成
- **pbi-agent**: PBI粒度への分解

### その他のエージェント

- **analyst-agent**: データ分析・改善提案
- **architect-agent**: ソース解析・技術仕様作成
- **feedback-agent**: フィードバック分析・PBI自動生成
- **pivot-agent**: ピボット評価・方向性変更の検知
- **integration-agent**: 全体調整・Notion連携
