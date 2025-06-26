# セットアップガイド

## 📋 概要

このガイドでは、共通開発ルール設定を任意のプロジェクトに適用する手順を説明します。

## 🚀 基本セットアップ

### 1. ルールファイルの配置

```bash
# このリポジトリをクローン
git clone <このリポジトリのURL> cursor-config

# あなたのプロジェクトにルールファイルをコピー
cp -r cursor-config/.cursor/ <プロジェクトディレクトリ>/

# 確認
ls <プロジェクトディレクトリ>/.cursor/rules/
```

### 2. 動作確認

Cursorエディタでプロジェクトを開き、以下を確認してください：

- [ ] 基本ルールが自動的に適用されている
- [ ] 日本語での対応が機能している
- [ ] 並列処理最適化が動作している

## 🎯 プロジェクトタイプ別セットアップ

### Webアプリケーション

```bash
# テンプレートを使用（推奨）
cp -r cursor-config/templates/web-app/ my-web-app/
cp -r cursor-config/.cursor/ my-web-app/
cd my-web-app
```

### APIサーバー

```bash
# テンプレートを使用（推奨）
cp -r cursor-config/templates/api-server/ my-api-server/
cp -r cursor-config/.cursor/ my-api-server/
cd my-api-server
```

### モバイルアプリ

```bash
# テンプレートを使用（推奨）
cp -r cursor-config/templates/mobile-app/ my-mobile-app/
cp -r cursor-config/.cursor/ my-mobile-app/
cd my-mobile-app
```

## ⚙️ カスタマイズ

### 1. プロジェクト固有ルールの追加

```bash
# 新しいルールファイルを作成
touch .cursor/rules/project-specific-rule.mdc
```

### 2. 既存ルールの修正

共通基本ルール（`common-base-rule.mdc`）は直接編集せず、追加のルールファイルで補完することを推奨します。

### 3. 技術スタック固有の設定

各技術スタックに特化したルールを追加する場合：

```bash
# React専用ルールの例
touch .cursor/rules/react-specific-rule.mdc

# Python専用ルールの例  
touch .cursor/rules/python-specific-rule.mdc
```

## 🔧 トラブルシューティング

### ルールが適用されない場合

1. `.cursor/rules/`ディレクトリが正しく配置されているか確認
2. Cursorエディタを再起動
3. プロジェクトを再度開く

### エラーが発生する場合

1. ルールファイルの構文を確認
2. YAMLフロントマターが正しいか確認
3. ファイル権限を確認

## 📞 サポート

問題が解決しない場合は、以下を確認してください：

- [使用例・サンプル](usage-examples.md)
- [カスタマイズガイド](customization-guide.md)
- プロジェクトのIssueページ 
