# AI-DLC: AI-Driven Life Cycle

プロダクト企画業務の完全自動化システム

## 概要

AI-DLC は、Kiro の機能（Hooks, Agents, Steering, MCP）を活用して、プロダクト企画業務を自動化するシステムです。

### 自動化される業務

1. **戦略立案** - 市場分析から KGI/KPI 設定まで
2. **PRD 作成** - 機能要件の詳細化
3. **バックログ生成** - エピック/ストーリー/タスクへの分解
4. **PBI 作成** - 見積もりと優先順位付け
5. **Notion 登録** - 自動的なプロジェクト管理
6. **ソース解析** - 技術仕様書と負債検出
7. **データ分析** - KPI 分析と改善提案
8. **タスク追加** - 突発タスクの自動統合
9. **フィードバック分析** - ユーザーの声から改善PBI自動生成
10. **ピボット評価** - プロダクト方向性変更の検知と評価
11. **既存プロジェクト取り込み** - 運用中プロジェクトのオンボーディング

## プロジェクト構造

```
.
├── .kiro/
│   ├── agents/              # 専門エージェント定義（JSON形式）
│   │   ├── strategy-agent.kiro.agent
│   │   ├── prd-agent.kiro.agent
│   │   ├── backlog-agent.kiro.agent
│   │   ├── analyst-agent.kiro.agent
│   │   ├── architect-agent.kiro.agent
│   │   ├── feedback-agent.kiro.agent
│   │   ├── pivot-agent.kiro.agent
│   │   └── integration-agent.kiro.agent
│   ├── hooks/               # 自動化トリガー（JSON形式）
│   │   ├── 01-new-project-strategy.kiro.hook
│   │   ├── 02-auto-prd-generation.kiro.hook
│   │   ├── 03-auto-backlog-generation.kiro.hook
│   │   ├── 04-auto-notion-sync.kiro.hook
│   │   ├── 05-weekly-analysis.kiro.hook
│   │   ├── 06-code-analysis.kiro.hook
│   │   ├── 07-adhoc-task-addition.kiro.hook
│   │   ├── 08-monthly-strategy-review.kiro.hook
│   │   ├── 09-feedback-analysis.kiro.hook
│   │   ├── 10-pivot-evaluation.kiro.hook
│   │   ├── 11-auto-feedback-to-pbi.kiro.hook
│   │   └── 12-existing-project-onboarding.kiro.hook
│   ├── steering/            # 自動化ルール
│   │   ├── product-planning-automation.md
│   │   └── agent-collaboration.md
│   └── settings/
│       └── mcp.json         # 外部連携設定
├── docs/
│   ├── strategy/            # 戦略ドキュメント
│   ├── prd/                 # PRD
│   ├── backlog/             # プロダクトバックログ
│   ├── pbi/                 # PBI JSON
│   ├── analysis/            # 分析レポート
│   ├── feedback/            # フィードバック分析
│   ├── pivot/               # ピボット評価
│   ├── onboarding/          # プロジェクトオンボーディング
│   ├── specs/               # 技術仕様書
│   └── templates/           # テンプレート
├── prompt_sample/           # プロンプトテンプレート
│   ├── 戦略立案フレームワーク.md
│   ├── 戦略的4階層プロダクト.md
│   └── prd作成.md
├── 戦略立案フレームワーク.md
├── 戦略的4階層プロダクト.md
├── prd作成.md
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

### 新規プロジェクト立ち上げ

1. Kiro のコマンドパレットを開く（Cmd+Shift+P）
2. "Open Kiro Hook UI"を選択
3. "🚀 新規プロジェクト戦略立案"を実行

または、チャットで：

```
@strategy-agent 新規プロジェクトの戦略立案を開始
```

### 自動フロー

戦略立案 → PRD 作成 → バックログ生成 → Notion 登録まで自動実行されます。

### 週次データ分析

Hook から"📊 週次データ分析"を実行、または：

```
@analyst-agent 週次データ分析を実行
```

### ソースコード解析

Hook から"🔍 ソースコード解析"を実行、または：

```
@architect-agent https://github.com/your-repo を解析
```

### 突発タスク追加

Hook から"➕ 突発タスク追加"を実行、または：

```
@backlog-agent 突発タスクを追加
タイトル: 〇〇機能の緊急修正
タイプ: Bug
緊急度: Critical
```

### 月次戦略レビュー

Hook から"🎯 月次戦略レビュー"を実行

### フィードバック分析

Hook から"📝 フィードバック分析"を実行、または：

```
@feedback-agent ユーザーフィードバックを分析
```

フィードバックファイルを `docs/feedback/` に配置すると自動分析されます。

### ピボット評価

Hook から"🔄 ピボット評価"を実行、または：

```
@pivot-agent プロダクトのピボット評価を実行
```

### 既存プロジェクトの取り込み

Hook から"🔗 既存プロジェクトオンボーディング"を実行

## エージェント一覧

| エージェント               | 役割                          | 呼び出し方           |
| :------------------------- | :---------------------------- | :------------------- |
| 戦略エージェント           | 市場分析・戦略立案            | `@strategy-agent`    |
| PRD エージェント           | 要求仕様書作成                | `@prd-agent`         |
| バックログエージェント     | タスク分解・優先順位付け      | `@backlog-agent`     |
| アナリストエージェント     | データ分析・改善提案          | `@analyst-agent`     |
| アーキテクトエージェント   | ソース解析・技術仕様          | `@architect-agent`   |
| フィードバックエージェント | ユーザーの声分析・PBI自動生成 | `@feedback-agent`    |
| ピボットエージェント       | 方向性変更の検知・評価        | `@pivot-agent`       |
| 統合エージェント           | 全体調整・Notion 連携         | `@integration-agent` |

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
