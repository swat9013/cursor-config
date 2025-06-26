# カスタマイズガイド

## 📝 概要

共通開発ルール設定をプロジェクトの特性に合わせてカスタマイズする方法を説明します。

## 🎯 カスタマイズの基本方針

### 1. 階層構造
- **共通基本ルール**: 全プロジェクト共通（変更非推奨）
- **技術スタック固有ルール**: 技術別の最適化
- **プロジェクト固有ルール**: 個別要件への対応

### 2. カスタマイズ原則
- **継承**: 既存ルールを基盤として追加・拡張
- **非破壊**: 共通ルールの直接編集を避ける
- **段階的**: 一度に多くの変更を行わない

## 🛠️ 技術スタック別カスタマイズ

### React + TypeScript

```mdc
---
name: "React TypeScript ルール"
type: "conditional"
description: "React + TypeScript プロジェクト用の最適化ルール"
version: "1.0.0"
tags: ["react", "typescript", "frontend"]
trigger_keywords: ["React", "TypeScript", "TSX", "コンポーネント"]
---

# React TypeScript 開発ルール

## コンポーネント設計原則
- 単一責任の原則に従う
- Props の型定義を必須とする
- デフォルトエクスポートよりも名前付きエクスポートを推奨

## Hook 使用規則
- useState の初期値には必ず型を指定
- useEffect の依存配列を必ず明記
- カスタムHook は use プレフィックスを使用
```

### Node.js + Express

```mdc
---
name: "Node.js Express ルール"
type: "conditional"
description: "Node.js + Express API開発用の最適化ルール"
version: "1.0.0"
tags: ["nodejs", "express", "api", "backend"]
trigger_keywords: ["Node.js", "Express", "API", "REST", "エンドポイント"]
---

# Node.js Express 開発ルール

## API設計原則
- RESTful な URL 構造を採用
- HTTP ステータスコードを適切に使用
- レスポンス形式を統一

## エラーハンドリング
- すべての非同期処理にエラーハンドリングを実装
- カスタムエラークラスを定義
- ログレベルを適切に設定
```

### Python + FastAPI

```mdc
---
name: "Python FastAPI ルール"
type: "conditional"
description: "Python + FastAPI 開発用の最適化ルール"
version: "1.0.0"
tags: ["python", "fastapi", "api", "backend"]
trigger_keywords: ["Python", "FastAPI", "Pydantic", "型ヒント"]
---

# Python FastAPI 開発ルール

## コーディング規約
- PEP 8 に準拠
- 型ヒントを必須とする
- docstring を必ず記載

## API設計
- Pydantic モデルでリクエスト/レスポンスを定義
- 依存性注入を積極的に活用
- 非同期処理を適切に使用
```

## 🎨 プロジェクト固有カスタマイズ

### 1. 業務固有ルールの追加

```mdc
---
name: "業務固有ルール"
type: "conditional"
description: "特定の業務領域に特化したルール"
version: "1.0.0"
tags: ["business", "domain-specific"]
trigger_keywords: ["業務", "ドメイン", "特定要件"]
---

# 業務固有開発ルール

## データ処理規則
- 個人情報は必ず暗号化
- ログには機密情報を出力しない
- データベースアクセスは専用クラスを経由

## セキュリティ要件
- 認証・認可を必須とする
- 入力値の検証を徹底
- セキュリティヘッダーを設定
```

### 2. チーム固有ルールの設定

```mdc
---
name: "チーム固有ルール"
type: "conditional"
description: "チーム特有の開発プロセスとルール"
version: "1.0.0"
tags: ["team", "process", "workflow"]
trigger_keywords: ["チーム", "プロセス", "レビュー"]
---

# チーム開発ルール

## コードレビュー規則
- 全てのコードは2人以上でレビュー
- レビューのチェックポイントを標準化
- セキュリティ観点のレビューを必須とする

## ブランチ戦略
- GitFlow を採用
- 機能ブランチは feature/ プレフィックス
- リリースブランチは release/ プレフィックス
```

## ⚙️ 高度なカスタマイズ

### 1. 条件付きルール適用

```mdc
---
name: "条件付きルール"
type: "conditional"
apply_if: 
  - file_extension: [".ts", ".tsx"]
  - directory_contains: ["package.json"]
  - env_var: "NODE_ENV=production"
---

# 本番環境固有ルール

## パフォーマンス要件
- バンドルサイズの最適化を必須とする
- 不要なコンソールログを削除
- プロダクションビルドでのソースマップ無効化
```

### 2. 動的ルール生成

```javascript
// .cursor/rules/dynamic-rule-generator.js
module.exports = {
  generateRules: (projectConfig) => {
    const rules = [];
    
    if (projectConfig.hasDatabase) {
      rules.push({
        name: "データベースルール",
        description: "データベース操作の最適化",
        rules: [
          "N+1クエリの回避",
          "インデックスの適切な使用",
          "トランザクション管理の徹底"
        ]
      });
    }
    
    if (projectConfig.isPublicAPI) {
      rules.push({
        name: "公開APIルール",
        description: "外部公開API用のセキュリティ強化",
        rules: [
          "レート制限の実装",
          "API キーによる認証",
          "入力値の厳格な検証"
        ]
      });
    }
    
    return rules;
  }
};
```

## 📋 カスタマイズのベストプラクティス

### 1. ルール作成時の注意点

#### ✅ 推奨
- 具体的で測定可能な基準を設定
- 例外条件を明確に定義
- 実装例を含める
- 定期的な見直しスケジュールを設定

#### ❌ 避けるべき
- 曖昧で主観的な表現
- 技術的制約を無視した理想論
- 過度に複雑な条件設定
- 他のルールとの矛盾

### 2. ルールのテストとバリデーション

```bash
# ルール適用テスト
cursor-rules-validator --config .cursor/rules/ --test-project ./test-project

# ルール矛盾チェック
cursor-rules-checker --check-conflicts .cursor/rules/

# パフォーマンス測定
cursor-rules-benchmark --rules .cursor/rules/ --iterations 100
```

### 3. バージョン管理とマイグレーション

```mdc
---
name: "ルールバージョン管理"
version: "2.1.0"
migration_from: "2.0.0"
breaking_changes:
  - "エラーハンドリングの必須化"
  - "型定義の厳格化"
migration_guide: |
  バージョン2.0.0からのマイグレーション手順：
  1. 既存のエラーハンドリングを確認
  2. 型定義の不足箇所を補完
  3. テストの実行とエラー修正
---
```

## 🔄 継続的改善プロセス

### 1. 効果測定

```javascript
// metrics-collector.js
const metrics = {
  codeQuality: {
    lintErrors: countLintErrors(),
    testCoverage: getTestCoverage(),
    codeComplexity: calculateComplexity()
  },
  productivity: {
    developmentSpeed: measureDevelopmentSpeed(),
    bugFixTime: calculateBugFixTime(),
    reviewTime: calculateReviewTime()
  }
};
```

### 2. フィードバック収集

```markdown
## ルール改善提案テンプレート

### 現在の問題
- 具体的な問題の説明
- 発生頻度と影響度
- 現在の回避方法

### 改善提案
- 具体的な改善案
- 期待される効果
- 実装の難易度

### 検証方法
- 改善効果の測定方法
- テスト手順
- ロールバック条件
```

### 3. コミュニティ貢献

```bash
# ルール共有
git clone https://github.com/your-org/cursor-rules-community
cp .cursor/rules/your-custom-rule.mdc cursor-rules-community/community-rules/
git add -A && git commit -m "Add custom rule for [specific use case]"
git push origin main
```

## 📞 サポートとトラブルシューティング

### よくある問題と解決方法

**Q: カスタムルールが適用されない**
A: ルールファイルの YAML フロントマターの構文を確認してください

**Q: ルール間で矛盾が発生する**
A: より具体的な trigger_keywords を設定し、適用条件を明確化してください

**Q: パフォーマンスが低下した**
A: ルールの複雑性を見直し、不要な処理を削除してください

### コミュニティサポート

- GitHub Issues: バグレポートや機能要求
- Discord チャンネル: リアルタイムサポート
- 月次勉強会: ベストプラクティス共有 
