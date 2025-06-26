# Webアプリケーション開発テンプレート

## 📝 概要

このテンプレートは、Webアプリケーション開発用に最適化された共通開発ルール設定です。

## 🎯 対象技術スタック

- **フロントエンド**: React, Vue.js, Angular, Svelte
- **TypeScript**: 型安全性の重視
- **バンドラー**: Vite, Webpack, Parcel
- **テスト**: Jest, Vitest, Cypress
- **CSS**: Tailwind CSS, styled-components, CSS Modules

## 🚀 セットアップ

```bash
# テンプレートを使用してプロジェクト作成
cp -r templates/web-app/ my-web-app/
cp -r .cursor/ my-web-app/
cd my-web-app

# 依存関係のインストール（例：npm）
npm install
```

## 📁 推奨プロジェクト構造

```
my-web-app/
├── src/
│   ├── components/          # 再利用可能なコンポーネント
│   │   ├── ui/             # 基本UIコンポーネント
│   │   └── features/       # 機能固有コンポーネント
│   ├── pages/              # ページコンポーネント
│   ├── hooks/              # カスタムフック
│   ├── utils/              # ユーティリティ関数
│   ├── services/           # API通信・外部サービス
│   ├── store/              # 状態管理
│   ├── types/              # TypeScript型定義
│   └── assets/             # 静的ファイル
├── public/                 # 公開静的ファイル
├── tests/                  # テストファイル
├── docs/                   # ドキュメント
└── .cursor/                # Cursorルール設定
```

## 🛠️ 含まれているルール

### 基本品質ルール
- TypeScript厳格モード
- ESLint + Prettier 統合
- 自動importソート
- 未使用コードの検出

### パフォーマンス最適化
- 動的インポートの推奨
- バンドルサイズ最適化
- 画像最適化ガイドライン
- メモ化の適切な使用

### セキュリティ
- XSS対策
- CSRF対策
- セキュアなAPI通信

## 📋 開発フロー例

### 1. 新機能開発

```plaintext
# 要件定義
「ユーザープロフィール画面の要件定義を作成して」

# 設計
「コンポーネント設計とAPI設計を検討して」

# 実装
「実装タスクに分割して、テストファーストで進めて」
```

### 2. コンポーネント開発

```plaintext
# コンポーネント設計
「再利用可能なボタンコンポーネントを設計して」

# Storybook 連携
「Storybookでコンポーネントドキュメントを作成して」

# テスト作成
「コンポーネントテストとアクセシビリティテストを作成して」
```

## 🔧 カスタマイズ例

### React専用設定

```mdc
---
name: "React最適化ルール"
type: "conditional"
trigger_keywords: ["React", "JSX", "Component"]
---

# React開発最適化

## Hooks使用規則
- useState の初期値は型を明確に指定
- useEffect の依存配列を必ず記載
- カスタムHookは use プレフィックス

## コンポーネント設計
- 単一責任原則の徹底
- Props drilling の回避
- 適切なメモ化の使用
```

### Vue.js専用設定

```mdc
---
name: "Vue.js最適化ルール"
type: "conditional"
trigger_keywords: ["Vue", "SFC", "Composition API"]
---

# Vue.js開発最適化

## Composition API 使用規則
- setup() 関数内でのロジック整理
- ref/reactive の適切な使い分け
- computed の積極的活用

## SFC 構造
- script setup の使用
- TypeScript with defineProps
- CSS scoped の必須使用
```

## 📊 品質メトリクス

### 推奨指標
- **テストカバレッジ**: 80%以上
- **バンドルサイズ**: 初期ロード250KB以下
- **Core Web Vitals**: 
  - LCP < 2.5s
  - FID < 100ms
  - CLS < 0.1

### パフォーマンス監視

```javascript
// performance-budget.config.js
module.exports = {
  budget: [
    {
      type: 'initial',
      maximumWarning: '250kb',
      maximumError: '350kb'
    },
    {
      type: 'anyComponentStyle',
      maximumWarning: '2kb',
      maximumError: '4kb'
    }
  ]
};
```

## 🧪 テスト戦略

### 1. 単体テスト
- コンポーネントテスト（React Testing Library等）
- ユーティリティ関数のテスト
- フック（Hook）のテスト

### 2. 統合テスト
- API連携テスト
- 状態管理テスト
- ルーティングテスト

### 3. E2Eテスト
- 主要ユーザーフローのテスト
- クロスブラウザテスト
- レスポンシブテスト

## 🚀 デプロイメント

### 静的サイトホスティング
- Netlify, Vercel, GitHub Pages
- 環境別設定管理
- CI/CD パイプライン

### コンテナ化
- Docker設定例
- Kubernetes デプロイ
- 環境変数管理

## 📚 参考リンク

- [React公式ドキュメント](https://react.dev/)
- [Vue.js公式ガイド](https://vuejs.org/guide/)
- [Web Performance最適化](https://web.dev/performance/)
- [アクセシビリティガイドライン](https://www.w3.org/WAI/WCAG21/quickref/) 
