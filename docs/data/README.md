# データディレクトリ

このディレクトリは、分析用データファイルを配置する場所です。

## 対応フォーマット

- **CSV**: KPIデータ、ユーザー行動ログ
- **JSON**: API レスポンス、イベントログ
- **Markdown**: フィードバック、インタビュー記録

## 自動取り込み

`docs/data/` 配下にファイルを配置すると、`data-sync-agent` が自動的に：

1. データを読み込み
2. 正規化処理
3. データ品質チェック
4. 分析用データセット生成
5. `@analyst-agent` を呼び出してKPI分析を実行

## ディレクトリ構造

```
docs/data/
├── README.md                    # このファイル
├── *.csv                        # 生データ（CSV）
├── *.json                       # 生データ（JSON）
├── normalized/                  # 正規化済みデータ
├── metadata/                    # データメタ情報
├── kpi-summary.json             # KPIサマリー
├── user-behavior.json           # ユーザー行動ログ
├── funnel-data.json             # ファネルデータ
├── notion-sync.json             # Notionデータ
├── github-metrics.json          # GitHubメトリクス
├── quality-report.md            # データ品質レポート
└── sync-report-{date}.md        # データ同期レポート
```

## データ例

### KPIデータ（CSV）

```csv
date,dau,mau,conversion_rate,retention_rate
2024-01-01,1000,5000,0.05,0.30
2024-01-02,1050,5100,0.052,0.31
```

### イベントログ（JSON）

```json
{
    "event": "user_signup",
    "timestamp": "2024-01-01T10:00:00Z",
    "user_id": "user123",
    "properties": {
        "source": "organic",
        "device": "mobile"
    }
}
```

## MCP経由のデータ取得

`@data-sync-agent` または Hook "📈 週次データ分析" を実行すると、MCP経由で以下のデータを自動取得：

- **Notion**: プロジェクト進捗、PBIステータス、スプリントベロシティ
- **GitHub**: Issue、PR、コミット履歴
- **その他**: 設定されたMCPデータソース

## 使い方

### 1. データファイルを配置

```bash
# CSVファイルをコピー
cp /path/to/kpi-data.csv docs/data/

# JSONファイルをコピー
cp /path/to/events.json docs/data/
```

### 2. 自動取り込みを待つ

ファイルが配置されると、Hook "📊 データファイル自動取り込み" が自動実行されます。

### 3. 手動で週次分析を実行

```bash
# Hook UIから "📈 週次データ分析" を実行
# または
@data-sync-agent 週次データ分析を開始
```

## データ品質チェック

自動的に以下をチェック：

- ✅ 必須カラムの存在確認
- ✅ データ型の妥当性
- ✅ 異常値の検出
- ✅ 重複データの確認

結果は `quality-report.md` に出力されます。
