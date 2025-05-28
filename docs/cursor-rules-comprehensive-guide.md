# Cursor Rules 包括的ガイドライン

## 目次
1. [Cursor Rulesとは](#cursor-rulesとは)
2. [ルールの種類と設定方法](#ルールの種類と設定方法)
3. [MDC形式での記述方法](#mdc形式での記述方法)
4. [YAML構造化記述のベストプラクティス](#yaml構造化記述のベストプラクティス)
5. [効果的なルール作成の原則](#効果的なルール作成の原則)
6. [実践的な応用例](#実践的な応用例)
7. [チーム運用での考慮事項](#チーム運用での考慮事項)
8. [トラブルシューティング](#トラブルシューティング)

## Cursor Rulesとは

Cursor Rulesは、AI開発アシスタントの動作をカスタマイズするための設定ファイルです。プロジェクト固有のコーディング規約、開発フロー、チーム文化を反映させることで、より効果的な開発支援を実現できます。

### 主な利点
- **一貫性の確保**: チーム全体で統一されたコーディングスタイル
- **効率性の向上**: プロジェクト固有の要件を事前に設定
- **品質の向上**: ベストプラクティスの自動適用
- **学習コストの削減**: 新メンバーへの知識伝達

## ルールの種類と設定方法

### 1. Project Rules（推奨）
プロジェクト固有のルールを`.cursor/rules`ディレクトリに保存

```
project-root/
├── .cursor/
│   └── rules/
│       ├── coding-standards.mdc
│       ├── architecture.mdc
│       └── team-workflow.mdc
```

### 2. User Rules
個人のグローバル設定（Cursor設定画面から管理）

### 3. .cursorrules（レガシー）
プロジェクトルートの単一ファイル（非推奨）

### ルールタイプ

#### Always
常に適用されるルール
```yaml
type: always
description: "基本的なコーディング規約"
```

#### Auto Attached
特定条件で自動適用
```yaml
type: auto_attached
conditions:
  - file_extensions: [".tsx", ".ts"]
  - directories: ["src/components"]
```

#### Agent Requested
エージェントが必要時に参照
```yaml
type: agent_requested
trigger_keywords: ["テスト", "デバッグ", "リファクタリング"]
```

#### Manual
手動で適用
```yaml
type: manual
description: "特殊な状況でのみ使用"
```

## MDC形式での記述方法

### 基本構造
```markdown
---
name: "コーディング規約"
type: "always"
description: "TypeScript/React プロジェクトの基本規約"
version: "1.0.0"
author: "開発チーム"
tags: ["typescript", "react", "coding-standards"]
---

# コーディング規約

## 基本方針
- 可読性を最優先とする
- 一貫性のあるコードスタイルを維持する
- TypeScriptの型安全性を活用する

## 具体的なルール
### 命名規則
- 変数名: camelCase
- 関数名: camelCase
- クラス名: PascalCase
- 定数: UPPER_SNAKE_CASE
```

### フロントマターの詳細設定
```yaml
---
name: "API開発ルール"
type: "auto_attached"
description: "REST API開発時の規約"
version: "2.1.0"
author: "バックエンドチーム"
created_at: "2024-01-15"
updated_at: "2024-03-20"
tags: ["api", "backend", "rest"]
conditions:
  file_extensions: [".py", ".js", ".ts"]
  directories: ["src/api", "backend"]
  file_patterns: ["*controller*", "*service*", "*model*"]
priority: 100
dependencies: ["database-rules.mdc", "security-rules.mdc"]
---
```

## YAML構造化記述のベストプラクティス

### 1. 階層構造の活用
```yaml
development_workflow:
  planning:
    - requirement_analysis: "要件を明確に定義する"
    - task_breakdown: "タスクを細分化する"
    - estimation: "工数を見積もる"
  
  implementation:
    - setup: "開発環境を準備する"
    - coding: "コーディング規約に従って実装する"
    - testing: "単体テストを作成・実行する"
  
  review:
    - self_check: "セルフレビューを実施する"
    - peer_review: "チームメンバーによるレビュー"
    - approval: "承認を得る"
```

### 2. 条件分岐の明確化
```yaml
code_review_process:
  small_changes:
    condition: "変更行数 < 50"
    reviewers: 1
    approval_required: false
  
  medium_changes:
    condition: "50 <= 変更行数 < 200"
    reviewers: 2
    approval_required: true
  
  large_changes:
    condition: "変更行数 >= 200"
    reviewers: 3
    approval_required: true
    architecture_review: true
```

### 3. テンプレートの分離
```yaml
templates:
  component_template: |
    import React from 'react';
    
    interface {{ComponentName}}Props {
      // プロパティを定義
    }
    
    export const {{ComponentName}}: React.FC<{{ComponentName}}Props> = (props) => {
      return (
        <div>
          {/* コンポーネントの実装 */}
        </div>
      );
    };
  
  test_template: |
    import { render, screen } from '@testing-library/react';
    import { {{ComponentName}} } from './{{ComponentName}}';
    
    describe('{{ComponentName}}', () => {
      it('should render correctly', () => {
        render(<{{ComponentName}} />);
        // テストの実装
      });
    });
```

## 効果的なルール作成の原則

### 1. 具体性の原則
❌ 悪い例：
```markdown
コードは綺麗に書いてください
```

✅ 良い例：
```yaml
code_quality_rules:
  function_length:
    max_lines: 20
    reason: "可読性と保守性の向上"
  
  variable_naming:
    pattern: "camelCase"
    examples:
      good: ["userName", "isActive", "calculateTotal"]
      bad: ["user_name", "IsActive", "calculate_total"]
```

### 2. 段階的確認の原則
```yaml
feature_development_process:
  step1_planning:
    action: "要件定義書を作成する"
    deliverable: "requirements.md"
    confirmation: "要件が明確に定義されているか確認"
  
  step2_design:
    action: "技術設計を行う"
    deliverable: "design.md"
    confirmation: "設計がアーキテクチャ方針に沿っているか確認"
  
  step3_implementation:
    action: "実装を開始する"
    deliverable: "動作するコード"
    confirmation: "テストが通ることを確認"
```

### 3. 例外処理の明確化
```yaml
error_handling:
  api_errors:
    network_error:
      action: "リトライ機構を実装"
      max_retries: 3
      backoff_strategy: "exponential"
    
    validation_error:
      action: "ユーザーフレンドリーなエラーメッセージを表示"
      log_level: "warn"
    
    server_error:
      action: "エラーページにリダイレクト"
      log_level: "error"
      notification: "開発チームに通知"
```

### 4. 文脈の提供
```yaml
project_context:
  technology_stack:
    frontend: "React 18 + TypeScript + Vite"
    backend: "Node.js + Express + PostgreSQL"
    testing: "Jest + React Testing Library"
    deployment: "Docker + AWS ECS"
  
  team_structure:
    frontend_team: 3
    backend_team: 2
    devops_team: 1
  
  business_domain: "Eコマースプラットフォーム"
  target_users: "中小企業の店舗運営者"
```

## 実践的な応用例

### 1. タスク管理エージェント
```yaml
---
name: "タスク管理アシスタント"
type: "agent_requested"
description: "効率的なタスク管理をサポート"
trigger_keywords: ["タスク", "TODO", "スケジュール"]
---

task_management:
  task_creation:
    required_fields:
      - title: "タスクの簡潔な説明"
      - priority: "High/Medium/Low"
      - estimated_time: "所要時間（時間）"
      - deadline: "期限（YYYY-MM-DD）"
      - assignee: "担当者"
    
    optional_fields:
      - description: "詳細説明"
      - dependencies: "依存タスク"
      - tags: "分類タグ"
  
  prioritization_criteria:
    high_priority:
      - "期限が24時間以内"
      - "ブロッカーとなるタスク"
      - "顧客影響が大きい"
    
    medium_priority:
      - "期限が1週間以内"
      - "計画されたリリースに含まれる"
    
    low_priority:
      - "改善・最適化タスク"
      - "技術的負債の解消"
  
  daily_workflow:
    morning_routine:
      - "前日の進捗確認"
      - "今日のタスク優先順位付け"
      - "ブロッカーの特定"
    
    evening_routine:
      - "完了タスクの記録"
      - "明日のタスク準備"
      - "進捗レポート作成"
```

### 2. コードレビューエージェント
```yaml
---
name: "コードレビューアシスタント"
type: "auto_attached"
conditions:
  file_extensions: [".ts", ".tsx", ".js", ".jsx"]
description: "コードレビューの品質向上をサポート"
---

code_review_checklist:
  functionality:
    - "要件通りに動作するか"
    - "エッジケースが考慮されているか"
    - "エラーハンドリングが適切か"
  
  code_quality:
    - "命名規則に従っているか"
    - "関数が単一責任を持っているか"
    - "重複コードがないか"
    - "適切なコメントがあるか"
  
  performance:
    - "不要な再レンダリングがないか"
    - "メモリリークの可能性はないか"
    - "効率的なアルゴリズムを使用しているか"
  
  security:
    - "入力値の検証が行われているか"
    - "機密情報がハードコードされていないか"
    - "適切な認証・認可が実装されているか"
  
  testing:
    - "単体テストが書かれているか"
    - "テストカバレッジが十分か"
    - "統合テストが必要か"

review_feedback_template: |
  ## レビュー結果
  
  ### 良い点
  - [具体的な良い実装を挙げる]
  
  ### 改善提案
  - [具体的な改善案を提示]
  
  ### 質問・確認事項
  - [不明な点や確認したい事項]
  
  ### 次のステップ
  - [修正後のアクション]
```

### 3. プロジェクト管理エージェント
```yaml
---
name: "プロジェクト管理アシスタント"
type: "manual"
description: "プロジェクト全体の進行管理をサポート"
---

project_phases:
  planning:
    duration: "2週間"
    deliverables:
      - "プロジェクト計画書"
      - "要件定義書"
      - "技術設計書"
      - "リスク分析書"
    
    key_activities:
      - stakeholder_meeting: "ステークホルダーとの要件確認"
      - technical_design: "アーキテクチャ設計"
      - resource_planning: "リソース計画策定"
      - risk_assessment: "リスク評価と対策立案"
  
  development:
    duration: "8週間"
    methodology: "アジャイル（2週間スプリント）"
    
    sprint_structure:
      sprint_planning:
        duration: "2時間"
        participants: ["開発チーム", "PO", "SM"]
        output: "スプリントバックログ"
      
      daily_standup:
        duration: "15分"
        format: "昨日やったこと、今日やること、ブロッカー"
      
      sprint_review:
        duration: "1時間"
        participants: ["開発チーム", "ステークホルダー"]
        output: "デモとフィードバック"
      
      retrospective:
        duration: "1時間"
        participants: ["開発チーム"]
        output: "改善アクション"

risk_management:
  technical_risks:
    - risk: "新技術の学習コスト"
      probability: "Medium"
      impact: "High"
      mitigation: "事前検証とプロトタイプ作成"
    
    - risk: "外部API依存"
      probability: "Low"
      impact: "High"
      mitigation: "代替案の準備とモックの活用"
  
  schedule_risks:
    - risk: "要件変更"
      probability: "High"
      impact: "Medium"
      mitigation: "変更管理プロセスの確立"
    
    - risk: "リソース不足"
      probability: "Medium"
      impact: "High"
      mitigation: "早期のリソース確保と外部委託検討"
```

### 4. メンタルサポートエージェント
```yaml
---
name: "開発者メンタルサポート"
type: "agent_requested"
description: "開発者の心理的サポートとモチベーション維持"
trigger_keywords: ["疲れた", "ストレス", "行き詰まり", "モチベーション"]
---

support_strategies:
  stress_management:
    recognition_signs:
      - "長時間の集中作業"
      - "エラーの頻発"
      - "コミュニケーションの減少"
      - "完璧主義的な発言"
    
    intervention_methods:
      immediate:
        - "5分間の休憩を提案"
        - "深呼吸エクササイズ"
        - "別のタスクへの切り替え"
      
      short_term:
        - "ペアプログラミングの提案"
        - "問題の細分化"
        - "チームメンバーへの相談推奨"
      
      long_term:
        - "ワークライフバランスの見直し"
        - "スキルアップ計画の策定"
        - "キャリア相談の機会提供"
  
  motivation_enhancement:
    achievement_recognition:
      - "小さな成功の積み重ねを評価"
      - "学習した新しいスキルの確認"
      - "チームへの貢献の可視化"
    
    goal_setting:
      - "SMART目標の設定支援"
      - "短期・中期・長期目標の整理"
      - "進捗の定期的な振り返り"
    
    learning_support:
      - "興味のある技術領域の探索"
      - "学習リソースの提案"
      - "実践機会の創出"

communication_templates:
  empathy_response: |
    お疲れ様です。{{situation}}で大変な状況ですね。
    まずは{{immediate_action}}をしてみませんか？
    その後、{{next_step}}について一緒に考えましょう。
  
  encouragement_message: |
    {{achievement}}を達成されましたね！素晴らしいです。
    特に{{specific_point}}の部分は、{{positive_impact}}につながっています。
    次は{{next_challenge}}に挑戦してみませんか？
  
  problem_solving_guide: |
    {{problem}}について整理してみましょう。
    
    1. 現状の把握：{{current_state}}
    2. 目標の明確化：{{desired_state}}
    3. 障害の特定：{{obstacles}}
    4. 解決策の検討：{{solutions}}
    5. 次のアクション：{{next_action}}
```

## チーム運用での考慮事項

### 1. ルールの共有と管理
```yaml
team_rule_management:
  version_control:
    - "Gitでルールファイルを管理"
    - "変更履歴の追跡"
    - "ブランチ戦略の適用"
  
  review_process:
    - "ルール変更のレビュー必須"
    - "チーム合意の取得"
    - "影響範囲の評価"
  
  documentation:
    - "ルールの目的と背景を記録"
    - "使用例とベストプラクティス"
    - "トラブルシューティングガイド"
```

### 2. 段階的導入戦略
```yaml
adoption_strategy:
  phase1_foundation:
    duration: "2週間"
    scope: "基本的なコーディング規約"
    success_criteria: "チーム全員が基本ルールを理解"
  
  phase2_workflow:
    duration: "4週間"
    scope: "開発ワークフローの標準化"
    success_criteria: "一貫したプロセスでの開発"
  
  phase3_advanced:
    duration: "継続的"
    scope: "高度な自動化とカスタマイズ"
    success_criteria: "生産性の向上と品質の安定化"
```

### 3. 効果測定
```yaml
effectiveness_metrics:
  code_quality:
    - "コードレビューでの指摘事項数"
    - "バグ発生率"
    - "技術的負債の蓄積度"
  
  productivity:
    - "開発速度（ストーリーポイント/スプリント）"
    - "リリース頻度"
    - "デプロイ成功率"
  
  team_satisfaction:
    - "開発者満足度調査"
    - "ルール遵守の負担感"
    - "改善提案の数"
```

## トラブルシューティング

### よくある問題と解決策

#### 1. ルールが適用されない
```yaml
troubleshooting:
  rule_not_applied:
    symptoms:
      - "期待した動作をしない"
      - "ルールが無視される"
    
    possible_causes:
      - "ファイルパスの設定ミス"
      - "条件設定の不備"
      - "優先度の競合"
    
    solutions:
      - "ファイルパスの確認"
      - "条件設定の見直し"
      - "ルールの優先度調整"
      - "Cursorの再起動"
```

#### 2. パフォーマンスの問題
```yaml
performance_issues:
  slow_response:
    causes:
      - "ルールファイルが大きすぎる"
      - "複雑な条件設定"
      - "循環参照"
    
    solutions:
      - "ルールの分割"
      - "条件の簡素化"
      - "依存関係の整理"
```

#### 3. チーム内での不整合
```yaml
team_inconsistency:
  different_behavior:
    causes:
      - "ルールのバージョン違い"
      - "個人設定の干渉"
      - "理解の相違"
    
    solutions:
      - "バージョン管理の徹底"
      - "定期的な同期"
      - "ドキュメントの充実"
```

## まとめ

効果的なCursor Rulesの作成には以下が重要です：

1. **明確性**: 曖昧さを排除し、具体的な指示を提供
2. **構造化**: YAML形式での論理的な整理
3. **段階性**: 確認ステップを含む段階的なプロセス
4. **実用性**: 実際の開発現場で使える内容
5. **保守性**: 継続的な改善と更新

このガイドラインを参考に、あなたのプロジェクトに最適なCursor Rulesを作成してください。 

## 参考文献

- [Cursor – Rules](https://docs.cursor.com/context/rules)
- [Cursorエージェント講座 超精度向上編。 Rulesテクニックであなたもエージェントマスターに！｜miyatti@エクスプラザ](https://note.com/miyatad/n/n18cfb4a4036c)
- [【保存版】明日から使える、組織のための Cursor Rules 運用](https://zenn.dev/kikagaku/articles/2d3752f773aa34)
