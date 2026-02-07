# AI-DLC: AI-Driven Life Cycle

プロダクト企画業務の完全自動化システム

## 概要

AI-DLC は、Kiro の機能（Hooks, Agents, Steering, MCP）を活用して、プロダクト企画業務を自動化するシステムです。

### 2つの企画アプローチ

#### A. 戦略立案アプローチ（トップダウン）

新規事業や大規模プロジェクト向け。市場分析から戦略立案を行います。

- **戦略立案** - 4階層フレームワーク（Core/Why/What/How）に基づく市場分析と戦略策定
- **PRD作成** - 戦略から機能要件への変換
- **バックログ生成** - エピック/ストーリー/タスクへの分解

#### B. 企画業務フロー（8ステップ）

既存事業の改善や機能追加向け。業務起点で要件を整理します。

1. **① 事業・課題インプット** - 事業課題の明文化、ターゲット定義、KGI/KPI設定
2. **② 企画スコープ定義** - プロダクト4階層整理、やる/やらないの決定
3. **③ 価値・体験整理** - UJM/インセプションデッキ作成
4. **④ 業務洗い出し** - ユーザー業務・運営業務の列挙
5. **⑤ 業務ロジック整理** - トリガー、判定条件、処理内容の定義
6. **⑥ 要件レベルへの翻訳** - 業務→システム要件への変換、PRD作成
7. **⑦ プロダクトバックログ作成** - エピック/ストーリー/タスクへの分解
8. **⑧ PBI粒度への分解** - 開発チームへの引き渡し準備

### C. スプリント運用・継続的改善

実運用に必要な機能を完備：

- **既存プロダクトオンボーディング** - 運用中プロダクトの取り込み、戦略・PRD・バックログの逆算生成
- **データ自動取り込み** - CSV/JSONファイル監視、MCP経由のデータ取得
- **週次データ分析** - KPI分析、トレンド分析、改善PBI自動生成
- **バックログリファインメント** - 見積もり精度確認、優先順位再評価
- **スプリント計画** - ベロシティベースのPBI選択、タスク分解
- **スプリントレトロスペクティブ** - Keep/Problem/Try整理、改善アクションのPBI化
- **バックログ修正** - 優先順位変更、PBI追加/削除、影響範囲分析
- **Notion連携** - PBIの自動登録とステータス同期
- **フィードバック分析** - ユーザーの声から改善PBI自動生成
- **ピボット評価** - プロダクト方向性変更の検知と評価

## プロジェクト構造

```
.
├── .kiro/
│   ├── agents/              # 専門エージェント定義（JSON形式）
│   │   ├── business-input-agent.kiro.agent          # ① 事業・課題インプット
│   │   ├── scope-definition-agent.kiro.agent        # ② 企画スコープ定義
│   │   ├── value-experience-agent.kiro.agent        # ③ 価値・体験整理
│   │   ├── business-process-agent.kiro.agent        # ④ 業務洗い出し
│   │   ├── business-logic-agent.kiro.agent          # ⑤ 業務ロジック整理
│   │   ├── requirements-agent.kiro.agent            # ⑥ 要件レベルへの翻訳
│   │   ├── product-backlog-agent.kiro.agent         # ⑦ プロダクトバックログ作成
│   │   ├── pbi-agent.kiro.agent                     # ⑧ PBI粒度への分解
│   │   ├── strategy-agent.kiro.agent                # 戦略立案（トップダウン）
│   │   ├── prd-agent.kiro.agent                     # PRD作成（戦略ベース）
│   │   ├── backlog-agent.kiro.agent                 # バックログ生成（戦略ベース）
│   │   ├── onboarding-agent.kiro.agent              # 既存プロダクトオンボーディング
│   │   ├── sprint-agent.kiro.agent                  # スプリント運用
│   │   ├── data-sync-agent.kiro.agent               # データ同期・取り込み
│   │   ├── analyst-agent.kiro.agent                 # データ分析
│   │   ├── architect-agent.kiro.agent               # ソース解析
│   │   ├── feedback-agent.kiro.agent                # フィードバック分析
│   │   ├── pivot-agent.kiro.agent                   # ピボット評価
│   │   └── integration-agent.kiro.agent             # Notion連携
│   ├── hooks/               # 自動化トリガー（JSON形式）
│   │   ├── 01-business-input.kiro.hook              # ① 事業・課題インプット
│   │   ├── 02-scope-definition.kiro.hook            # ② 企画スコープ定義
│   │   ├── 03-value-experience.kiro.hook            # ③ 価値・体験整理
│   │   ├── 04-business-process.kiro.hook            # ④ 業務洗い出し
│   │   ├── 05-business-logic.kiro.hook              # ⑤ 業務ロジック整理
│   │   ├── 06-requirements.kiro.hook                # ⑥ 要件レベルへの翻訳
│   │   ├── 07-product-backlog.kiro.hook             # ⑦ プロダクトバックログ作成
│   │   ├── 08-pbi-breakdown.kiro.hook               # ⑧ PBI粒度への分解
│   │   ├── 01-new-project-strategy.kiro.hook        # 戦略立案（トップダウン）
│   │   ├── 09-feedback-analysis.kiro.hook           # フィードバック分析
│   │   ├── 10-pivot-evaluation.kiro.hook            # ピボット評価
│   │   ├── 11-data-file-sync.kiro.hook              # データファイル自動取り込み
│   │   ├── 12-weekly-data-analysis.kiro.hook        # 週次データ分析
│   │   ├── 13-existing-product-onboarding.kiro.hook # 既存プロダクトオンボーディング
│   │   ├── 14-backlog-refinement.kiro.hook          # バックログリファインメント
│   │   ├── 15-sprint-planning.kiro.hook             # スプリント計画
│   │   ├── 16-sprint-retrospective.kiro.hook        # スプリントレトロスペクティブ
│   │   └── 17-backlog-update.kiro.hook              # バックログ修正
│   ├── steering/            # 自動化ルール
│   │   ├── planning-workflow.md                     # 企画業務フロー
│   │   ├── product-planning-automation.md           # 企画自動化
│   │   └── agent-collaboration.md                   # エージェント協調
│   └── settings/
│       └── mcp.json         # 外部連携設定
├── docs/
│   ├── strategy/            # 戦略ドキュメント（トップダウン）
│   ├── input/               # ① 事業・課題インプット
│   ├── scope/               # ② 企画スコープ定義
│   ├── experience/          # ③ 価値・体験整理（UJM）
│   ├── process/             # ④ 業務洗い出し
│   ├── logic/               # ⑤ 業務ロジック整理
│   ├── prd/                 # ⑥ PRD（要件定義）
│   ├── backlog/             # ⑦ プロダクトバックログ
│   ├── pbi/                 # ⑧ PBI詳細
│   ├── data/                # 分析データ（CSV/JSON）
│   ├── analysis/            # データ分析レポート
│   ├── sprint/              # スプリント計画・レビュー・レトロ
│   ├── onboarding/          # 既存プロダクトオンボーディング
│   ├── feedback/            # フィードバック分析
│   ├── specs/               # 技術仕様書
│   └── templates/           # テンプレート
├── prompt_sample/           # プロンプトテンプレート
│   ├── 戦略立案フレームワーク.md
│   ├── 戦略的4階層プロダクト.md
│   └── prd作成.md
├── README.md
└── QUICKSTART.md
```

## セットアップ

### 1. MCP 設定

`.kiro/settings/mcp.json`に環境変数を設定：

```bash
export NOTION_API_KEY="your-notion-api-key"
export GITHUB_TOKEN="your-github-token"
```

### 2. Notion データベース作成

以下の 3 つのデータベースを Notion に作成：

#### プロジェクト DB

- プロジェクト名（Title）
- ステータス（Select）
- 戦略ドキュメント（URL）
- PRD（URL）
- KGI（Text）

#### エピック DB

- エピック名（Title）
- プロジェクト（Relation → プロジェクト DB）
- 優先度（Select: High/Medium/Low）
- ステータス（Select）

#### PBI DB

- タイトル（Title）
- タイプ（Select: User Story/Task/Bug）
- エピック（Relation → エピック DB）
- ストーリーポイント（Number）
- 優先度（Select）
- ステータス（Select: To Do/In Progress/Done）
- 担当者（Person）
- スプリント（Text）

## 使い方

### A. 戦略立案アプローチ（新規事業・大規模プロジェクト）

1. Kiro のコマンドパレットを開く（Cmd+Shift+P）
2. "Open Kiro Hook UI"を選択
3. "🚀 新規プロジェクト戦略立案"を実行

または、チャットで：

```
@strategy-agent 新規プロジェクトの戦略立案を開始
```

**自動フロー**: 戦略立案 → PRD作成 → バックログ生成 → Notion登録

---

### B. 企画業務フロー（既存事業改善・機能追加）

1. Kiro のコマンドパレットを開く（Cmd+Shift+P）
2. "Open Kiro Hook UI"を選択
3. "① 事業・課題インプット"を実行

または、チャットで：

```
@business-input-agent 新規プロジェクトの事業・課題インプットを開始
```

**自動フロー**: ① 事業・課題インプット → ② 企画スコープ定義 → ③ 価値・体験整理 → ④ 業務洗い出し → ⑤ 業務ロジック整理 → ⑥ 要件レベルへの翻訳（PRD作成） → ⑦ プロダクトバックログ作成 → ⑧ PBI粒度への分解 → Notion登録

---

### 各ステップの個別実行

#### 戦略立案アプローチ

```bash
# 戦略立案
@strategy-agent 新規プロジェクトの戦略立案を開始

# PRD作成（戦略ベース）
@prd-agent docs/strategy/[project]-strategy.md を読み込んでPRD作成

# バックログ生成（戦略ベース）
@backlog-agent docs/prd/[project]-prd.md を読み込んでバックログ作成
```

#### 企画業務フロー（8ステップ）

```bash
# ① 事業・課題インプット
@business-input-agent プロジェクト名: [名前] で事業・課題インプットを開始

# ② 企画スコープ定義
@scope-definition-agent docs/input/[project]-business-input.md を読み込んでスコープ定義

# ③ 価値・体験整理
@value-experience-agent UJMとインセプションデッキを作成

# ④ 業務洗い出し
@business-process-agent ユーザー業務と運営業務を洗い出し

# ⑤ 業務ロジック整理
@business-logic-agent 業務ロジックを詳細化

# ⑥ 要件レベルへの翻訳
@requirements-agent PRDを作成

# ⑦ プロダクトバックログ作成
@product-backlog-agent バックログを作成

# ⑧ PBI粒度への分解
@pbi-agent PBIを詳細化して開発チームに引き渡し
```

#### スプリント運用・継続的改善

```bash
# 既存プロダクトオンボーディング
@onboarding-agent 既存プロダクトをAI-DLCに取り込み

# データファイル配置（自動取り込み）
# docs/data/ にCSV/JSONファイルを配置すると自動的に取り込まれます

# 週次データ分析（MCP経由）
@data-sync-agent 週次データ分析を開始

# バックログリファインメント
@sprint-agent バックログリファインメントを実施

# スプリント計画
@sprint-agent スプリント計画を開始

# スプリントレトロスペクティブ
@sprint-agent スプリントレトロスペクティブを実施

# バックログ修正
@sprint-agent バックログを修正

# データ分析
@analyst-agent KPI分析を実行

# ソースコード解析
@architect-agent https://github.com/your-repo を解析

# フィードバック分析
@feedback-agent ユーザーフィードバックを分析

# ピボット評価
@pivot-agent プロダクトのピボット評価を実行
```

## エージェント一覧

### A. 戦略立案アプローチ（トップダウン）

| エージェント           | 役割                                          | 呼び出し方        |
| :--------------------- | :-------------------------------------------- | :---------------- |
| 戦略エージェント       | 4階層フレームワークに基づく市場分析・戦略立案 | `@strategy-agent` |
| PRDエージェント        | 戦略から機能要件への変換、世界基準のPRD作成   | `@prd-agent`      |
| バックログエージェント | PRDからエピック/ストーリー/タスクへの分解     | `@backlog-agent`  |

### B. 企画業務フロー（8ステップ）

| エージェント               | 役割                                        | 呼び出し方                |
| :------------------------- | :------------------------------------------ | :------------------------ |
| ① 事業・課題インプット     | 事業課題明文化、ターゲット定義、KGI/KPI設定 | `@business-input-agent`   |
| ② 企画スコープ定義         | プロダクト4階層整理、やる/やらない決定      | `@scope-definition-agent` |
| ③ 価値・体験整理           | UJM/インセプションデッキ作成                | `@value-experience-agent` |
| ④ 業務洗い出し             | ユーザー業務・運営業務の列挙                | `@business-process-agent` |
| ⑤ 業務ロジック整理         | トリガー、判定条件、処理内容の定義          | `@business-logic-agent`   |
| ⑥ 要件レベルへの翻訳       | 業務→システム要件変換、PRD作成              | `@requirements-agent`     |
| ⑦ プロダクトバックログ作成 | エピック/ストーリー/タスク分解              | `@product-backlog-agent`  |
| ⑧ PBI粒度への分解          | 開発チームへの引き渡し準備                  | `@pbi-agent`              |

### C. スプリント運用・継続的改善

| エージェント                 | 役割                               | 呼び出し方           |
| :--------------------------- | :--------------------------------- | :------------------- |
| オンボーディングエージェント | 既存プロダクトの取り込み、逆算生成 | `@onboarding-agent`  |
| スプリントエージェント       | スプリント計画・レビュー・レトロ   | `@sprint-agent`      |
| データ同期エージェント       | データ取り込み、MCP連携            | `@data-sync-agent`   |
| アナリストエージェント       | データ分析・改善提案               | `@analyst-agent`     |
| アーキテクトエージェント     | ソース解析・技術仕様               | `@architect-agent`   |
| フィードバックエージェント   | ユーザーの声分析・PBI自動生成      | `@feedback-agent`    |
| ピボットエージェント         | 方向性変更の検知・評価             | `@pivot-agent`       |
| 統合エージェント             | 全体調整・Notion連携               | `@integration-agent` |

## フレームワーク

### 戦略立案

- 4 階層フレームワーク（Core/Why/What/How）
- MECE 思考
- 因数分解
- フェルミ推定

### PRD 作成

- 機能要件（MoSCoW 優先順位）
- 非機能要件
- ユーザーフロー
- 受け入れ基準

### バックログ管理

- エピック → ユーザーストーリー → タスク
- ストーリーポイント見積もり
- 依存関係管理

## トラブルシューティング

### MCP サーバーが起動しない

```bash
# uvのインストール確認
uv --version

# インストールされていない場合
curl -LsSf https://astral.sh/uv/install.sh | sh
```

### Notion 連携エラー

1. NOTION_API_KEY が正しく設定されているか確認
2. Notion インテグレーションがデータベースにアクセス権を持っているか確認
3. MCP サーバーを再起動: Kiro Feature Panel → MCP Server → Reconnect

### エージェントが応答しない

1. `.kiro/agents/`に`.kiro.agent`ファイルがあるか確認
2. Kiroを再起動
3. チャットで明示的にエージェントを呼び出す（例: `@strategy-agent`）

### Hooksが表示されない

1. `.kiro/hooks/`に`.kiro.hook`ファイルがあるか確認
2. Kiroを再起動
3. コマンドパレット → "Open Kiro Hook UI"で確認

## カスタマイズ

### 新しいエージェントの追加

`.kiro/agents/your-agent.kiro.agent`を作成：

```json
{
    "name": "your-agent",
    "description": "エージェントの説明",
    "tools": ["read", "write"],
    "allowedTools": ["read", "write"],
    "resources": ["file://docs/**/*.md", "file://.kiro/steering/**/*.md"],
    "prompt": "あなたの役割と専門領域を記述...",
    "model": "claude-sonnet-4"
}
```

### 新しいHookの追加

`.kiro/hooks/your-hook.kiro.hook`を作成：

```json
{
    "enabled": true,
    "name": "Hook名",
    "description": "Hookの説明",
    "version": "1",
    "when": {
        "type": "userTriggered"
    },
    "then": {
        "type": "askAgent",
        "agent": "your-agent",
        "prompt": "実行する内容..."
    }
}
```

または、コマンドパレット → "Open Kiro Hook UI"から作成

## ライセンス

MIT
