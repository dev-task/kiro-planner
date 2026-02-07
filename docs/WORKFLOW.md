# 企画業務フロー詳細

このドキュメントでは、AI-DLCの企画業務8ステップの詳細なワークフローを説明します。

## 全体フロー図

```
┌─────────────────────────────────────────────────────────────┐
│                    ① 事業・課題インプット                      │
│              @business-input-agent                          │
│  ・事業課題明文化 ・ターゲット定義 ・KGI/KPI設定              │
└────────────────────┬────────────────────────────────────────┘
                     │ business-input.md
                     ↓
┌─────────────────────────────────────────────────────────────┐
│                    ② 企画スコープ定義                         │
│            @scope-definition-agent                          │
│  ・4階層整理 ・やる/やらない決定 ・フェーズ分割               │
└────────────────────┬────────────────────────────────────────┘
                     │ scope.md
                     ↓
┌─────────────────────────────────────────────────────────────┐
│                    ③ 価値・体験整理                           │
│            @value-experience-agent                          │
│  ・UJM作成 ・インセプションデッキ ・Aha Moment特定            │
└────────────────────┬────────────────────────────────────────┘
                     │ ujm.md
                     ↓
┌─────────────────────────────────────────────────────────────┐
│                    ④ 業務洗い出し                             │
│            @business-process-agent                          │
│  ・ユーザー業務列挙 ・運営業務列挙 ・自動化/人対応分類        │
└────────────────────┬────────────────────────────────────────┘
                     │ business-process.md
                     ↓
┌─────────────────────────────────────────────────────────────┐
│                    ⑤ 業務ロジック整理                         │
│            @business-logic-agent                            │
│  ・トリガー定義 ・判定条件 ・処理内容 ・状態変化              │
└────────────────────┬────────────────────────────────────────┘
                     │ business-logic.md
                     ↓
┌─────────────────────────────────────────────────────────────┐
│                  ⑥ 要件レベルへの翻訳                         │
│              @requirements-agent                            │
│  ・業務→システム要件変換 ・PRD作成 ・非機能要件整理           │
└────────────────────┬────────────────────────────────────────┘
                     │ prd.md
                     ↓
┌─────────────────────────────────────────────────────────────┐
│                ⑦ プロダクトバックログ作成                      │
│            @product-backlog-agent                           │
│  ・エピック/ストーリー/タスク分解 ・優先度付け ・依存関係整理  │
└────────────────────┬────────────────────────────────────────┘
                     │ backlog.md
                     ↓
┌─────────────────────────────────────────────────────────────┐
│                  ⑧ PBI粒度への分解                           │
│                  @pbi-agent                                 │
│  ・PBI詳細化 ・受入条件付与 ・開発チームへ引き渡し            │
└────────────────────┬────────────────────────────────────────┘
                     │ pbi.md / pbi.json
                     ↓
┌─────────────────────────────────────────────────────────────┐
│                    Notion自動登録                             │
│              @integration-agent                             │
│  ・プロジェクトDB ・エピックDB ・PBI DB                       │
└─────────────────────────────────────────────────────────────┘
```

## 各ステップの詳細

### ① 事業・課題インプット

**目的**: 企画の前提を揃える

**入力**: ユーザーからの情報

**処理**:

1. プロジェクト名の確認
2. 解くべき事業課題のヒアリング
3. ターゲットユーザーの定義
4. KGI/KPIの設定
5. 制約条件（期間・予算・体制）の整理

**出力**: `docs/input/{project-name}-business-input.md`

**トリガー**: 手動実行（Hook UI または @business-input-agent）

---

### ② 企画スコープ定義

**目的**: やる／やらないを決める

**入力**: `docs/input/{project-name}-business-input.md`

**処理**:

1. プロダクト4階層（Core/Why/What/How）の整理
2. 対象とする価値・機能群の決定
3. 今回作らないものリストの作成
4. フェーズ分割（MVP/v1/v2）

**出力**: `docs/scope/{project-name}-scope.md`

**トリガー**: business-input.md作成時に自動実行

---

### ③ 価値・体験整理

**目的**: ユーザー視点を固定する

**入力**:

- `docs/input/{project-name}-business-input.md`
- `docs/scope/{project-name}-scope.md`

**処理**:

1. ユーザージャーニーマップ（UJM）作成
2. 各フェーズの価値・課題明示
3. 成功体験（Aha Moment）の特定
4. 失敗体験（離脱ポイント）の分析
5. インセプションデッキ作成

**出力**: `docs/experience/{project-name}-ujm.md`

**トリガー**: scope.md作成時に自動実行

---

### ④ 業務洗い出し

**目的**: 体験を「業務」に変換する

**入力**: `docs/experience/{project-name}-ujm.md`

**処理**:

1. ユーザー業務の列挙
2. 運営業務（CS・運用）の列挙
3. 自動化／人対応の分類
4. 通常系／例外系の分類

**出力**: `docs/process/{project-name}-business-process.md`

**トリガー**: ujm.md作成時に自動実行

---

### ⑤ 業務ロジック整理

**目的**: 仕様の芯を作る

**入力**: `docs/process/{project-name}-business-process.md`

**処理**:
業務ごとに以下を定義：

1. トリガー（何をきっかけに開始するか）
2. 主体（誰がやるか）
3. 判定条件（どんな条件で分岐するか）
4. 処理内容（何をするか）
5. 状態変化（結果どうなるか）
6. 重要な分岐・例外の明確化

**出力**: `docs/logic/{project-name}-business-logic.md`

**トリガー**: business-process.md作成時に自動実行

---

### ⑥ 要件レベルへの翻訳

**目的**: 業務 → 要件に落とす

**入力**:

- `docs/logic/{project-name}-business-logic.md`
- `docs/scope/{project-name}-scope.md`

**処理**:

1. 業務ロジック → システム要件への変換
2. 必要な画面・API・データの整理
3. 非機能要件（性能・権限・ログ）整理
4. MVPで実装する範囲の確定
5. PRD作成

**出力**: `docs/prd/{project-name}-prd.md`

**トリガー**: business-logic.md作成時に自動実行

---

### ⑦ プロダクトバックログ作成

**目的**: 開発できる単位に並べる

**入力**: `docs/prd/{project-name}-prd.md`

**処理**:

1. 要件をバックログアイテム化
2. エピック → ユーザーストーリー → タスクへの分解
3. ビジネス価値で優先度付け
4. MVP順に並び替え
5. 依存関係の整理
6. スプリント計画（案）作成

**出力**: `docs/backlog/{project-name}-backlog.md`

**トリガー**: prd.md作成時に自動実行

---

### ⑧ PBI粒度への分解

**目的**: 開発チームが迷わず着手できる状態にする

**入力**: `docs/backlog/{project-name}-backlog.md`

**処理**:

1. バックログアイテムをPBI粒度に分割
2. 各PBIに以下を付与：
    - 背景（なぜ必要か）
    - 受入条件（Doneの定義）
    - 業務ルール・制約
    - 依存関係
    - 技術メモ
3. 開発チームと認識合わせ可能な状態にする

**出力**:

- `docs/pbi/{project-name}-pbi.md`（Markdown形式）
- `docs/pbi/{project-name}-pbi.json`（Notion API用）

**トリガー**: backlog.md作成時に自動実行

**次のステップ**: @integration-agent を呼び出してNotion登録

---

## Notion自動登録

**目的**: PBIをNotionで管理可能にする

**入力**: `docs/pbi/{project-name}-pbi.json`

**処理**:

1. プロジェクトDBへの登録
2. エピックDBへの登録
3. PBI DBへの登録
4. リレーション設定

**出力**: Notionデータベースへの登録完了

**トリガー**: pbi-agent完了後に自動呼び出し

---

## 途中から再開する方法

特定のステップから開始したい場合：

```bash
# ② から開始
@scope-definition-agent docs/input/[project]-business-input.md を読み込んでスコープ定義

# ③ から開始
@value-experience-agent docs/scope/[project]-scope.md を読み込んでUJM作成

# ④ から開始
@business-process-agent docs/experience/[project]-ujm.md を読み込んで業務洗い出し

# ⑤ から開始
@business-logic-agent docs/process/[project]-business-process.md を読み込んで業務ロジック整理

# ⑥ から開始
@requirements-agent docs/logic/[project]-business-logic.md を読み込んでPRD作成

# ⑦ から開始
@product-backlog-agent docs/prd/[project]-prd.md を読み込んでバックログ作成

# ⑧ から開始
@pbi-agent docs/backlog/[project]-backlog.md を読み込んでPBI詳細化
```

## ファイル修正後の再実行

途中のファイルを修正した場合、次のエージェントを手動で呼び出すことで、修正内容を反映した続きのステップを実行できます。

例：

1. `docs/scope/{project}-scope.md` を修正
2. `@value-experience-agent` を呼び出して③以降を再実行

## 並行実行

複数のプロジェクトを同時に進める場合、プロジェクト名を変えることで並行実行が可能です。

```
プロジェクトA: @business-input-agent プロジェクト名: ProjectA で開始
プロジェクトB: @business-input-agent プロジェクト名: ProjectB で開始
```
