# Full-Stack Web Application Constitution
<!-- Node.js + Python + TypeScript 混在プロジェクト -->

## Core Principles

### I. 多言語協調開発 (Multi-Language Harmonization)
- **Node.js (TypeScript)**: フロントエンド・API・リアルタイム機能
- **Python**: データ処理・機械学習・バックエンドロジック・科学計算
- 言語選択はタスクの特性に基づく；既存の専門知識・ライブラリエコシステム・パフォーマンス要件を考慮
- 共通のインターフェース規約：REST API、JSON通信、統一ログフォーマット

### II. GitHub Copilot 駆動開発
- GitHub Copilot を開発の中核ツールとして位置づけ
- Spec Kit を使用した仕様駆動開発：`/specify` → `/plan` → `/tasks` → 実装
- 仕様書・計画書・タスクリストはすべてGitHub Copilot で生成・更新
- コード生成・リファクタリング・テスト作成にGitHub Copilot を積極活用

### III. テスト駆動開発 (NON-NEGOTIABLE)
- **TDD必須**: テスト設計 → ユーザー承認 → テスト失敗 → 実装 → テスト成功
- **Node.js**: Jest/Vitest + Testing Library でユニット・結合テスト
- **Python**: pytest + fixtures でユニット・結合テスト  
- **E2E**: Playwright でブラウザテスト自動化
- Red-Green-Refactor サイクルを厳格に実施

### IV. フルスタック統合テスト
- **API契約テスト**: OpenAPI仕様に基づくスキーマ検証
- **言語間通信テスト**: Node.js ↔ Python 間のデータ整合性
- **データベース統合**: マイグレーション・シード・ロールバックテスト
- **認証・認可**: エンドツーエンドセキュリティテスト

### V. 監視可能性とトレーサビリティ
- **構造化ログ**: JSON形式で統一（Node.js: winston, Python: structlog）
- **メトリクス収集**: アプリケーション・インフラレベル両方
- **エラー追跡**: スタックトレース・コンテキスト・ユーザー影響の記録
- **パフォーマンス監視**: レスポンス時間・メモリ使用量・CPU使用率

## 技術スタック規約

### フロントエンド
- **言語**: TypeScript（必須）、JavaScript（レガシー対応のみ）
- **フレームワーク**: React + Next.js（SSR/SSG）、Vue.js（単一コンポーネント）
- **スタイリング**: Tailwind CSS + CSS Modules
- **ビルドツール**: Vite または Next.js標準ビルダー

### バックエンド
- **Node.js**: Express.js + TypeScript、FastAPI風のルーティング
- **Python**: FastAPI（Web API）、Django（管理系）、Flask（軽量API）
- **データベース**: PostgreSQL（主）、Redis（キャッシュ・セッション）
- **ORM**: Prisma（Node.js）、SQLAlchemy（Python）

### 開発・デプロイ環境
- **コンテナ**: Docker + Docker Compose（開発・ステージング）
- **CI/CD**: GitHub Actions + 自動テスト・デプロイ
- **インフラ**: クラウドネイティブ（AWS/Azure/GCP）
- **モニタリング**: Application Insights / CloudWatch / Prometheus

## 品質保証・セキュリティ

### コード品質
- **リンター**: ESLint（TS/JS）、Black + Flake8（Python）
- **フォーマッター**: Prettier（TS/JS）、Black（Python）
- **型安全性**: TypeScript strict mode、Python typing + mypy
- **コードレビュー**: PRベース、自動品質チェック必須

### セキュリティ要件
- **認証**: OAuth 2.0 + JWT、多要素認証対応
- **認可**: RBAC（ロールベースアクセス制御）
- **データ保護**: GDPR/個人情報保護法準拠、暗号化（保存時・転送時）
- **脆弱性管理**: Dependabot、定期セキュリティ監査

### パフォーマンス基準
- **レスポンス時間**: API < 200ms、ページロード < 3秒
- **可用性**: 99.9%アップタイム（ダウンタイム < 8.76時間/年）
- **スケーラビリティ**: 水平スケールアウト対応設計
- **リソース効率**: メモリ使用量最適化、データベースクエリ最適化

## Governance
この憲章はすべての開発プラクティスに優先する；
修正には文書化・承認・移行計画が必要；
すべてのPR・レビューで準拠性を検証；
複雑性は必ず正当化が必要；
runtime開発ガイダンスは `.specify/templates/` を参照；

**Version**: 1.0.0 | **Ratified**: 2025-01-15 | **Last Amended**: 2025-01-15