# クイックスタート

AI-DLC を 5 分で始める

## 1. 環境変数の設定

```bash
# Notion API Key（必須）
export NOTION_API_KEY="secret_xxxxxxxxxxxxx"

# GitHub Token（オプション）
export GITHUB_TOKEN="ghp_xxxxxxxxxxxxx"
```

### Notion API Key の取得方法

1. https://www.notion.so/my-integrations にアクセス
2. "New integration"をクリック
3. 名前を入力（例: AI-DLC）
4. "Submit"をクリック
5. "Internal Integration Token"をコピー

### Notion データベースの準備

1. Notion で新しいページを作成
2. 以下の 3 つのデータベースを作成：
    - **Projects** (プロジェクト管理)
    - **Epics** (エピック管理)
    - **PBIs** (バックログアイテム)
3. 各データベースで"..."メニュー → "Add connections" → "AI-DLC"を選択

## 2. MCP サーバーの起動確認

```bash
# uvがインストールされているか確認
uv --version

# インストールされていない場合
curl -LsSf https://astral.sh/uv/install.sh | sh
```

Kiro で：

1. Feature Panel（サイドバー）を開く
2. "MCP Servers"セクションを確認
3. "notion", "github", "filesystem"が"Connected"になっているか確認

## 3. 最初のプロジェクトを作成

### 方法1: Hookから実行（推奨）

1. Cmd+Shift+P でコマンドパレットを開く
2. "Open Kiro Hook UI"を入力
3. "🚀 新規プロジェクト戦略立案"をクリック
4. 対話形式でプロジェクト情報を入力

**利用可能なHooks:**

- 🚀 新規プロジェクト戦略立案
- 📊 週次データ分析
- 🔍 ソースコード解析
- ➕ 突発タスク追加
- 🎯 月次戦略レビュー

### 方法2: チャットから実行

Kiroチャットで：

```
@strategy-agent 新規プロジェクトの戦略立案を開始してください。

プロジェクト名: タスク管理アプリ
解決したい課題: チームのタスク管理が煩雑で、進捗が見えにくい
ターゲット: 10-50人規模のスタートアップ
```

**利用可能なエージェント:**

- `@strategy-agent` - 戦略立案
- `@prd-agent` - PRD作成
- `@backlog-agent` - バックログ管理
- `@analyst-agent` - データ分析
- `@architect-agent` - ソース解析
- `@integration-agent` - Notion連携

## 4. 自動フローの確認

以下が自動的に実行されます：

1. ✅ 戦略ドキュメント生成 → `docs/strategy/`
2. ✅ PRD 生成 → `docs/prd/`
3. ✅ バックログ生成 → `docs/backlog/`
4. ✅ PBI JSON 生成 → `docs/pbi/`
5. ✅ Notion に自動登録

## 5. Notion で確認

Notion のデータベースを開いて、プロジェクト・エピック・PBI が登録されているか確認

## よくある質問

### Q: エージェントが応答しない

A:

1. `.kiro/agents/`フォルダに`.kiro.agent`ファイルがあるか確認
2. Kiroを再起動
3. チャットで`@エージェント名`で明示的に呼び出す（例: `@strategy-agent`）

### Q: Notion 連携が失敗する

A:

1. NOTION_API_KEY が正しく設定されているか確認
2. Notion データベースにインテグレーションが接続されているか確認
3. MCP サーバーを再起動（Feature Panel → MCP Servers → Reconnect）

### Q: 既存プロジェクトに適用できる？

A: はい。以下のコマンドで既存リポジトリを解析できます：

```
@architect-agent https://github.com/your-org/your-repo を解析
```

### Q: Hooksが表示されない

A:

1. `.kiro/hooks/`フォルダに`.kiro.hook`ファイルがあるか確認
2. Kiroを再起動
3. コマンドパレット（Cmd+Shift+P） → "Open Kiro Hook UI"で確認

## 次のステップ

- [README.md](README.md) - 詳細なドキュメント
- [docs/WORKFLOW.md](docs/WORKFLOW.md) - ワークフロー詳細
- [docs/EXAMPLES.md](docs/EXAMPLES.md) - 実行例
- [prompt_sample/戦略立案フレームワーク.md](prompt_sample/戦略立案フレームワーク.md) - 戦略立案の詳細
- [prompt_sample/prd作成.md](prompt_sample/prd作成.md) - PRD作成の詳細

## サポート

問題が発生した場合は、以下を確認：

1. `.kiro/`フォルダの構造
2. MCP サーバーの接続状態
3. 環境変数の設定
4. Kiro のログ（Output Panel → Kiro）
