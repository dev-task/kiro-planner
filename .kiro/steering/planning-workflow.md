---
inclusion: auto
---

# 企画業務フロー自動化ルール

このステアリングルールは、企画担当の業務フロー（〜プロダクトバックログアイテム洗い出しまで）を自動化するための指針です。

## 企画業務の8ステップ

```
① 事業・課題インプット
  ↓
② 企画スコープ定義
  ↓
③ 価値・体験整理
  ↓
④ 業務洗い出し
  ↓
⑤ 業務ロジック整理
  ↓
⑥ 要件レベルへの翻訳
  ↓
⑦ プロダクトバックログ作成
  ↓
⑧ PBI粒度への分解（開発引き渡し）
```

## 各工程の詳細

### ① 事業・課題インプット

**目的**: 企画の前提を揃える

**やること**:

- 解くべき事業課題を明文化
- ターゲットユーザー定義
- 成功指標（KGI / KPI）設定
- 制約条件（期間・予算・体制）整理

**アウトプット**: `docs/input/{project-name}-business-input.md`

**担当エージェント**: @business-input-agent

**トリガー**: Hook "① 事業・課題インプット" を手動実行

---

### ② 企画スコープ定義

**目的**: やる／やらないを決める

**やること**:

- プロダクト4階層の整理（Core/Why/What/How）
- 対象とする価値・機能群を決定
- フェーズ分割（MVP / v1 / v2）

**アウトプット**: `docs/scope/{project-name}-scope.md`

**担当エージェント**: @scope-definition-agent

**トリガー**: `docs/input/*-business-input.md` 作成時に自動実行

---

### ③ 価値・体験整理（UJM / インセプション）

**目的**: ユーザー視点を固定する

**やること**:

- ユーザー行動を時系列で洗い出し
- 各フェーズの価値・課題を明示
- 成功体験・失敗体験を言語化

**アウトプット**: `docs/experience/{project-name}-ujm.md`

**担当エージェント**: @value-experience-agent

**トリガー**: `docs/scope/*-scope.md` 作成時に自動実行

---

### ④ 業務洗い出し

**目的**: 体験を「業務」に変換する

**やること**:

- ユーザー業務を列挙
- 運営業務（CS・運用）を列挙
- 自動化／人対応を分ける
- 通常系／例外系を分ける

**アウトプット**: `docs/process/{project-name}-business-process.md`

**担当エージェント**: @business-process-agent

**トリガー**: `docs/experience/*-ujm.md` 作成時に自動実行

---

### ⑤ 業務ロジック整理

**目的**: 仕様の芯を作る（超重要）

**やること**:
業務ごとに以下を定義：

- トリガー
- 主体（誰がやるか）
- 判定条件
- 処理内容
- 状態変化
- 重要な分岐・例外を明確化

**アウトプット**: `docs/logic/{project-name}-business-logic.md`

**担当エージェント**: @business-logic-agent

**トリガー**: `docs/process/*-business-process.md` 作成時に自動実行

---

### ⑥ 要件レベルへの翻訳

**目的**: 業務 → 要件に落とす

**やること**:

- 業務ロジックを「システム要件」に変換
- 必要な画面・API・データを整理
- 非機能要件（性能・権限・ログ）整理
- MVPで実装する範囲を確定

**アウトプット**: `docs/prd/{project-name}-prd.md`

**担当エージェント**: @requirements-agent

**トリガー**: `docs/logic/*-business-logic.md` 作成時に自動実行

---

### ⑦ プロダクトバックログ作成

**目的**: 開発できる単位に並べる

**やること**:

- 要件をバックログアイテム化
- ビジネス価値で優先度付け
- MVP順に並び替え
- 依存関係を整理

**アウトプット**: `docs/backlog/{project-name}-backlog.md`

**担当エージェント**: @product-backlog-agent

**トリガー**: `docs/prd/*-prd.md` 作成時に自動実行

---

### ⑧ PBI粒度への分解（開発引き渡し）

**目的**: 開発チームが迷わず着手できる状態にする

**やること**:

- バックログアイテムをPBI粒度に分割
- 各PBIに以下を付与：
    - 背景（なぜ必要か）
    - 受入条件（Doneの定義）
    - 業務ルール・制約
- 開発チームと認識合わせ

**アウトプット**:

- `docs/pbi/{project-name}-pbi.md`
- `docs/pbi/{project-name}-pbi.json`

**担当エージェント**: @pbi-agent

**トリガー**: `docs/backlog/*-backlog.md` 作成時に自動実行

**次のステップ**: @integration-agent を呼び出してNotion登録

---

## 自動化の流れ

1. ユーザーがHook "① 事業・課題インプット" を手動実行
2. @business-input-agent がユーザーに質問して情報収集
3. `docs/input/{project-name}-business-input.md` を作成
4. 以降、ファイル作成をトリガーに自動的に次のステップが実行される
5. 最終的に `docs/pbi/{project-name}-pbi.json` が生成される
6. @integration-agent がNotionに自動登録

## ディレクトリ構造

```
docs/
├── input/              # ① 事業・課題インプット
├── scope/              # ② 企画スコープ定義
├── experience/         # ③ 価値・体験整理（UJM）
├── process/            # ④ 業務洗い出し
├── logic/              # ⑤ 業務ロジック整理
├── prd/                # ⑥ 要件レベルへの翻訳
├── backlog/            # ⑦ プロダクトバックログ
└── pbi/                # ⑧ PBI粒度への分解
```

## 参考フレームワーク

- #[[file:prompt_sample/戦略立案フレームワーク.md]]
- #[[file:prompt_sample/戦略的4階層プロダクト.md]]
- #[[file:prompt_sample/prd作成.md]]
