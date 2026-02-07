---
inclusion: always
---

# エージェント協調ルール

このステアリングルールは、複数のエージェントが協調して動作する際の指針です。

## エージェント呼び出し規約

### 明示的呼び出し

ユーザーまたは他のエージェントが`@agent-name`で明示的に呼び出した場合、そのエージェントが応答します。

### 自動連携

特定のエージェントが完了した際、次のエージェントを自動的に呼び出します：

```
① business-input-agent完了 → @scope-definition-agent を自動呼び出し
② scope-definition-agent完了 → @value-experience-agent を自動呼び出し
③ value-experience-agent完了 → @business-process-agent を自動呼び出し
④ business-process-agent完了 → @business-logic-agent を自動呼び出し
⑤ business-logic-agent完了 → @requirements-agent を自動呼び出し
⑥ requirements-agent完了 → @product-backlog-agent を自動呼び出し
⑦ product-backlog-agent完了 → @pbi-agent を自動呼び出し
⑧ pbi-agent完了 → @integration-agent を自動呼び出し
```

## データ受け渡し

### ファイルベース

エージェント間のデータ受け渡しは、主にファイル経由で行います：

```
① business-input-agent → docs/input/{project}-business-input.md
② scope-definition-agent → docs/scope/{project}-scope.md
③ value-experience-agent → docs/experience/{project}-ujm.md
④ business-process-agent → docs/process/{project}-business-process.md
⑤ business-logic-agent → docs/logic/{project}-business-logic.md
⑥ requirements-agent → docs/prd/{project}-prd.md
⑦ product-backlog-agent → docs/backlog/{project}-backlog.md
⑧ pbi-agent → docs/pbi/{project}-pbi.md
                → docs/pbi/{project}-pbi.json
```

### コンテキスト共有

前のエージェントの出力ファイルを次のエージェントが読み込みます。

## エージェントの責任範囲

各エージェントは自分の専門領域に集中し、他の領域には踏み込みません：

- **business-input-agent**: 事業課題の明文化のみ。スコープ決定には踏み込まない
- **scope-definition-agent**: スコープ定義のみ。体験設計には踏み込まない
- **value-experience-agent**: UJM/体験整理のみ。業務詳細には踏み込まない
- **business-process-agent**: 業務洗い出しのみ。ロジック詳細には踏み込まない
- **business-logic-agent**: 業務ロジックのみ。システム要件には踏み込まない
- **requirements-agent**: 要件定義のみ。バックログ優先順位には踏み込まない
- **product-backlog-agent**: バックログ作成のみ。PBI詳細化には踏み込まない
- **pbi-agent**: PBI詳細化のみ。実装方法には踏み込まない
- **analyst-agent**: 分析のみ。意思決定には踏み込まない
- **architect-agent**: 技術仕様のみ。ビジネス判断には踏み込まない
- **integration-agent**: 連携のみ。各領域の専門判断には踏み込まない

## エラーハンドリング

### エージェント失敗時

あるエージェントが失敗した場合、統合エージェントがフォールバック処理を実行します。

### データ不整合時

データの不整合を検出した場合、警告を発し、前のエージェントに修正を依頼します。

## 並行実行

以下のエージェントは並行実行可能です：

- analyst-agent + architect-agent
- 複数のプロジェクトの企画フロー（異なるプロジェクト名）
- feedback-agent + pivot-agent

## 優先順位

複数のエージェントが同時に実行要求された場合の優先順位：

1. Critical Bug 対応（緊急タスク）
2. 企画フローの継続（①→⑧の順次実行）
3. データ分析（analyst-agent）
4. フィードバック分析（feedback-agent）
5. ソース解析（architect-agent）
6. ピボット評価（pivot-agent）
