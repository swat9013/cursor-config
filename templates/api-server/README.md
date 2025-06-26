# APIサーバー開発テンプレート

## 📝 概要

このテンプレートは、APIサーバー開発用に最適化された共通開発ルール設定です。

## 🎯 対象技術スタック

- **Node.js**: Express, Fastify, Koa
- **Python**: FastAPI, Django REST, Flask
- **Java**: Spring Boot, Jersey
- **Go**: Gin, Echo, Chi
- **C#**: ASP.NET Core Web API

## 🚀 セットアップ

```bash
# テンプレートを使用してプロジェクト作成
cp -r templates/api-server/ my-api-server/
cp -r .cursor/ my-api-server/
cd my-api-server
```

## 📁 推奨プロジェクト構造

```
my-api-server/
├── src/
│   ├── controllers/        # リクエストハンドラー
│   ├── services/           # ビジネスロジック
│   ├── repositories/       # データアクセス層
│   ├── models/             # データモデル
│   ├── middleware/         # ミドルウェア
│   ├── routes/             # ルーティング定義
│   ├── utils/              # ユーティリティ
│   ├── config/             # 設定ファイル
│   └── types/              # 型定義（TypeScript）
├── tests/                  # テストファイル
├── docs/                   # API仕様書
├── scripts/                # デプロイ・管理スクリプト
├── docker/                 # Docker設定
└── .cursor/                # Cursorルール設定
```

## 🛠️ 含まれているルール

### API設計規則
- RESTful URL設計
- HTTP ステータスコード統一
- レスポンス形式標準化
- バージョニング戦略

### セキュリティ強化
- 入力値検証
- 認証・認可実装
- レート制限
- セキュリティヘッダー設定

### エラーハンドリング
- 統一されたエラーレスポンス
- 適切なログ出力
- 障害時の復旧処理

## 📋 開発フロー例

### 1. API設計

```plaintext
# 要件定義
「ユーザー管理APIの要件定義を作成して」

# API仕様設計
「RESTful APIの設計方針を検討して」
「OpenAPI仕様書を作成して」

# 実装計画
「エンドポイント実装タスクに分割して」
```

### 2. エンドポイント実装

```plaintext
# CRUD操作
「ユーザーCRUD APIを実装して」
「データベース連携を含めて設計して」

# 認証機能
「JWT認証機能を実装して」
「セキュリティ要件を満たして」

# テスト作成
「APIテストとセキュリティテストを作成して」
```

## 🔧 言語別カスタマイズ例

### Node.js + Express

```mdc
---
name: "Node.js Express API ルール"
type: "conditional"
trigger_keywords: ["Node.js", "Express", "API", "middleware"]
---

# Node.js Express 開発最適化

## ミドルウェア設計
- 責務の単一化
- エラーハンドリングミドルウェアの統一
- 非同期処理の適切な処理

## セキュリティ実装
- helmet.js によるセキュリティヘッダー
- cors 設定の適切な管理
- rate-limit による制限
```

### Python + FastAPI

```mdc
---
name: "Python FastAPI ルール"  
type: "conditional"
trigger_keywords: ["Python", "FastAPI", "Pydantic", "async"]
---

# Python FastAPI 開発最適化

## 型定義
- Pydantic モデルの活用
- 型ヒントの必須使用
- レスポンスモデルの定義

## 非同期処理
- async/await の適切な使用
- データベース接続プールの管理
- バックグラウンドタスクの実装
```

### Java + Spring Boot

```mdc
---
name: "Java Spring Boot API ルール"
type: "conditional" 
trigger_keywords: ["Java", "Spring Boot", "Controller", "Service"]
---

# Java Spring Boot 開発最適化

## レイヤーアーキテクチャ
- Controller-Service-Repository パターン
- 依存性注入の適切な使用
- トランザクション管理

## 例外処理
- カスタム例外クラスの定義
- GlobalExceptionHandler の実装
- 適切なHTTPステータス返却
```

## 📊 API品質メトリクス

### パフォーマンス指標
- **レスポンス時間**: 95%tile < 200ms
- **スループット**: 1000 RPS以上
- **エラー率**: < 0.1%

### セキュリティ指標
- **認証成功率**: > 99.5%
- **不正アクセス検出率**: > 95%
- **データ暗号化**: 100%

## 🧪 テスト戦略

### 1. 単体テスト
```javascript
// Controller テスト例
describe('UserController', () => {
  test('GET /users/:id should return user', async () => {
    const response = await request(app)
      .get('/users/1')
      .expect(200);
    
    expect(response.body).toMatchObject({
      id: 1,
      name: expect.any(String),
      email: expect.any(String)
    });
  });
});
```

### 2. 統合テスト
```javascript
// API統合テスト例
describe('User API Integration', () => {
  test('Create -> Read -> Update -> Delete flow', async () => {
    // Create
    const createResponse = await request(app)
      .post('/users')
      .send({ name: 'Test User', email: 'test@example.com' })
      .expect(201);
    
    const userId = createResponse.body.id;
    
    // Read
    await request(app)
      .get(`/users/${userId}`)
      .expect(200);
    
    // Update
    await request(app)
      .put(`/users/${userId}`)
      .send({ name: 'Updated User' })
      .expect(200);
    
    // Delete
    await request(app)
      .delete(`/users/${userId}`)
      .expect(204);
  });
});
```

### 3. セキュリティテスト
```javascript
// セキュリティテスト例
describe('Security Tests', () => {
  test('should reject unauthorized requests', async () => {
    await request(app)
      .get('/users/1')
      .expect(401);
  });
  
  test('should validate input parameters', async () => {
    await request(app)
      .post('/users')
      .send({ name: '', email: 'invalid-email' })
      .expect(400);
  });
});
```

## 🗄️ データベース設計指針

### 1. 関係データベース (PostgreSQL, MySQL)
- 正規化の適切な適用
- インデックス戦略
- トランザクション設計

### 2. NoSQL (MongoDB, DynamoDB)
- スキーマ設計原則
- クエリパフォーマンス最適化
- データ整合性戦略

### 3. キャッシュ戦略
- Redis/Memcached活用
- キャッシュ無効化戦略
- パフォーマンス監視

## 🔐 セキュリティベストプラクティス

### 認証・認可
```javascript
// JWT実装例
const jwt = require('jsonwebtoken');

const authenticateToken = (req, res, next) => {
  const authHeader = req.headers['authorization'];
  const token = authHeader && authHeader.split(' ')[1];
  
  if (!token) {
    return res.sendStatus(401);
  }
  
  jwt.verify(token, process.env.ACCESS_TOKEN_SECRET, (err, user) => {
    if (err) return res.sendStatus(403);
    req.user = user;
    next();
  });
};
```

### 入力値検証
```python
# FastAPI バリデーション例
from pydantic import BaseModel, validator
from typing import Optional

class UserCreate(BaseModel):
    name: str
    email: str
    age: Optional[int] = None
    
    @validator('email')
    def validate_email(cls, v):
        if '@' not in v:
            raise ValueError('Invalid email format')
        return v
    
    @validator('age')
    def validate_age(cls, v):
        if v is not None and (v < 0 or v > 150):
            raise ValueError('Age must be between 0 and 150')
        return v
```

## 🚀 デプロイメント戦略

### コンテナ化
```dockerfile
# Multi-stage Dockerfile例
FROM node:18-alpine AS builder
WORKDIR /app
COPY package*.json ./
RUN npm ci --only=production

FROM node:18-alpine AS runtime
WORKDIR /app
COPY --from=builder /app/node_modules ./node_modules
COPY . .
EXPOSE 3000
USER node
CMD ["npm", "start"]
```

### CI/CD パイプライン
```yaml
# GitHub Actions例
name: API Deploy
on:
  push:
    branches: [main]

jobs:
  test:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v3
      - name: Run tests
        run: npm test
  
  deploy:
    needs: test
    runs-on: ubuntu-latest
    steps:
      - name: Deploy to production
        run: |
          docker build -t api-server .
          docker push registry/api-server:latest
```

## 📚 参考リンク

- [REST API設計ガイド](https://restfulapi.net/)
- [OpenAPI仕様](https://swagger.io/specification/)
- [API Security Checklist](https://github.com/shieldfy/API-Security-Checklist)
- [Node.js Best Practices](https://github.com/goldbergyoni/nodebestpractices) 
