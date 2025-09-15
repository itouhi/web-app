# Spec Kit 導入・運用ガイド

> **GitHub Copilot での仕様駆動開発 完全ガイド**

このガイドでは、GitHub Spec Kit を使用した仕様駆動開発の導入から日常運用まで、実践的な内容を詳しく解説します。

## 📋 目次

1. [概要](#概要)
2. [クイックスタート](#クイックスタート)
3. [詳細セットアップ](#詳細セットアップ)
4. [基本的な使用方法](#基本的な使用方法)
5. [実践例](#実践例)
6. [よくある質問 (FAQ)](#よくある質問-faq)
7. [トラブルシューティング](#トラブルシューティング)
8. [運用・保守](#運用保守)

## 📖 概要

### Spec Kit とは

GitHub Spec Kit は、GitHub が2024年9月に発表した仕様駆動開発（Spec-Driven Development）を支援するツールキットです。GitHub Copilot と統合することで、自然言語の要求から実装可能なコードまでの変換を効率化します。

### 主な特徴

- **要求 → 仕様 → 計画 → タスク** の段階的な開発フロー
- **GitHub Copilot カスタムコマンド** との統合
- **プロジェクト特化のテンプレート** 機能
- **品質保証メカニズム** (Constitution Check)
- **多言語・フレームワーク対応**

### 対象読者

- GitHub Copilot を使用している開発者
- 仕様駆動開発に興味がある開発チーム
- 要求分析から実装までの効率化を図りたいプロジェクト

## 🚀 クイックスタート

### 5分でセットアップ

#### 1. 前提条件の確認

```bash
# Python 3.11+ の確認
python --version
# Expected: Python 3.11.0 以上

# uv パッケージマネージャーの確認
uv --version
# Expected: uv 0.8.17 以上
```

#### 2. Spec Kit のインストール

```bash
# GitHub Copilot 向けの初期化
uvx --from git+https://github.com/github/spec-kit.git specify init --here --ai copilot

# システムチェック実行
uvx --from git+https://github.com/github/spec-kit.git specify check
```

#### 3. VS Code での確認

1. VS Code を開く
2. `Ctrl+Shift+P` (macOS: `Cmd+Shift+P`) でコマンドパレットを開く
3. "GitHub Copilot: /" と入力
4. `/specify`, `/plan`, `/tasks` コマンドが表示されることを確認

### 最初の実行

```bash
# VS Code で以下を実行
/specify ユーザー登録機能を作りたい
```

成功すると、`specs/` ディレクトリに仕様書が生成されます。

## 🔧 詳細セットアップ

### 環境要件

#### 必須要件

| 項目 | 要件 | 確認方法 |
|------|------|----------|
| OS | Linux/macOS/WSL2 | `uname -a` |
| Python | 3.11+ | `python --version` |
| uv | 0.8.17+ | `uv --version` |
| Git | 2.0+ | `git --version` |
| GitHub Copilot | 有効 | VS Code で確認 |

#### 推奨要件

| 項目 | 推奨バージョン | 用途 |
|------|----------------|------|
| Node.js | 18+ | TypeScript プロジェクト |
| Docker | 最新 | コンテナ開発 |
| VS Code | 最新 | 主要開発環境 |

### インストール手順詳細

#### 1. uv のインストール (未インストールの場合)

```bash
# Linux/macOS
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows (PowerShell)
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"

# 環境変数の更新
source ~/.bashrc  # または ~/.zshrc
```

#### 2. Spec Kit の初期化オプション

```bash
# 基本的な初期化 (GitHub Copilot 向け)
uvx --from git+https://github.com/github/spec-kit.git specify init --here --ai copilot

# カスタムオプション付き初期化
uvx --from git+https://github.com/github/spec-kit.git specify init \
  --here \
  --ai copilot \
  --script bash \
  --debug
```

#### 3. プロジェクト固有の設定

```bash
# プロジェクト憲法のカスタマイズ
edit .specify/constitution.md

# テンプレートの調整
edit .specify/templates/spec_template.md
edit .specify/templates/plan_template.md
edit .specify/templates/tasks_template.md
```

### VS Code 統合設定

#### 1. 拡張機能の確認

必要な拡張機能:
- **GitHub Copilot** (必須)
- **GitHub Copilot Chat** (推奨)
- **Python** (Python プロジェクトの場合)
- **TypeScript** (TypeScript プロジェクトの場合)

#### 2. 設定ファイルの最適化

`.vscode/settings.json`:
```json
{
  "github.copilot.enable": {
    "*": true,
    "markdown": true,
    "plaintext": true
  },
  "github.copilot.advanced": {
    "listCount": 10,
    "inlineSuggestCount": 3
  }
}
```

## 🛠️ 基本的な使用方法

### GitHub Copilot コマンド

#### `/specify` - 仕様作成

**用途**: 自然言語の要求を構造化された仕様書に変換

```bash
# 基本的な使用
/specify ユーザー認証システムを作りたい

# 詳細な要求
/specify 
APIキーベースの認証システムを実装したい。
- JWT トークンの発行・検証
- ユーザー登録・ログイン
- パスワードリセット機能
- Node.js + TypeScript で実装
```

**出力**: `specs/{YYYYMMDD-HHMMSS}-{title}/spec.md`

#### `/plan` - 実装計画作成

**用途**: 仕様書から具体的な実装計画を生成

```bash
# 仕様書を指定して計画作成
/plan specs/20240915-143000-user-auth/spec.md
```

**出力**: `specs/{YYYYMMDD-HHMMSS}-{title}/plan.md`

#### `/tasks` - 実装タスク作成

**用途**: 実装計画から具体的なコーディングタスクを生成

```bash
# 計画書を指定してタスク作成
/tasks specs/20240915-143000-user-auth/plan.md
```

**出力**: `specs/{YYYYMMDD-HHMMSS}-{title}/tasks.md`

### 基本的なワークフロー

#### 1. 要求分析 → 仕様作成

```markdown
# VS Code で実行
/specify 
Node.js + Python 混在の Web API を作りたい。
- Node.js でフロントエンド API
- Python でバックエンド処理
- Redis でセッション管理
- PostgreSQL でデータ永続化
```

#### 2. 仕様確認・調整

生成された `spec.md` を確認し、必要に応じて手動調整:

```markdown
# specs/YYYYMMDD-HHMMSS-web-api/spec.md
## 要件
- 高性能な API レスポンス (<100ms)
- 同時接続 1000+ 対応
- セキュリティ対策 (HTTPS, CORS, Rate Limiting)

## アーキテクチャ
...
```

#### 3. 実装計画の生成

```bash
/plan specs/YYYYMMDD-HHMMSS-web-api/spec.md
```

#### 4. 計画確認・調整

生成された `plan.md` をレビュー:

```markdown
# specs/YYYYMMDD-HHMMSS-web-api/plan.md
## フェーズ 1: 基盤構築
1. プロジェクト構造の作成
2. 依存関係のセットアップ
3. 開発環境の構築

## フェーズ 2: API実装
...
```

#### 5. 実装タスクの生成

```bash
/tasks specs/YYYYMMDD-HHMMSS-web-api/plan.md
```

#### 6. タスク実装

生成された `tasks.md` を元に GitHub Copilot で実装:

```markdown
# specs/YYYYMMDD-HHMMSS-web-api/tasks.md
## タスク 1: Express.js セットアップ
- [ ] package.json の作成
- [ ] Express.js のインストール
- [ ] 基本的なサーバー設定

## タスク 2: データベース接続
...
```

## 🎯 実践例

### 例1: REST API の開発

#### Step 1: 要求定義

```bash
/specify 
ブログシステムのREST APIを作成したい。
要件:
- 記事の CRUD 操作
- カテゴリー管理
- ユーザー認証
- 検索機能
- Node.js + TypeScript
- PostgreSQL + Prisma
```

#### Step 2: 生成された仕様の確認

```markdown
## API 仕様

### エンドポイント
- GET /api/posts - 記事一覧取得
- POST /api/posts - 記事作成
- GET /api/posts/:id - 記事詳細取得
- PUT /api/posts/:id - 記事更新
- DELETE /api/posts/:id - 記事削除

### データモデル
```typescript
interface Post {
  id: string
  title: string
  content: string
  authorId: string
  categoryId: string
  createdAt: Date
  updatedAt: Date
}
```
```

#### Step 3: 実装計画の生成

```bash
/plan specs/20240915-151200-blog-api/spec.md
```

#### Step 4: タスク実装

```bash
/tasks specs/20240915-151200-blog-api/plan.md
```

### 例2: バグ修正・機能改善

#### Step 1: 現状分析

```bash
/specify 
現在のユーザー認証システムにおいて、
パスワードリセット機能でメール送信が失敗する問題を修正したい。

現在の実装:
- Node.js + Express
- SendGrid を使用
- JWT トークンでの認証

問題:
- SendGrid APIキーの設定エラー
- メールテンプレートの文字化け
- レート制限の考慮不足
```

#### Step 2: 修正計画

```bash
/plan specs/20240915-152000-password-reset-fix/spec.md
```

#### Step 3: 修正タスク

```bash
/tasks specs/20240915-152000-password-reset-fix/plan.md
```

## ❓ よくある質問 (FAQ)

### Q1: GitHub Copilot コマンドが認識されない

**A**: 以下を確認してください:

1. **Spec Kit の初期化確認**
   ```bash
   uvx --from git+https://github.com/github/spec-kit.git specify check
   ```

2. **VS Code の再起動**
   ```bash
   # VS Code を完全に終了して再起動
   ```

3. **GitHub Copilot の有効化確認**
   - VS Code で `Ctrl+Shift+P` → "GitHub Copilot: Check Status"

### Q2: 生成される仕様が不正確・不完全

**A**: 以下の方法で改善できます:

1. **より詳細な要求入力**
   ```bash
   /specify 
   具体的な要件:
   - 技術スタック: Node.js + TypeScript
   - データベース: PostgreSQL
   - 認証方式: JWT
   - API形式: REST
   - テスト: Jest + Supertest
   ```

2. **Constitution の調整**
   ```bash
   edit .specify/constitution.md
   # プロジェクト固有の制約・ガイドラインを追加
   ```

3. **段階的詳細化**
   ```bash
   # 1. 大まかな仕様作成
   /specify システム全体の概要
   
   # 2. 個別機能の詳細化
   /specify ユーザー認証機能の詳細
   ```

### Q3: 多言語プロジェクトでの設定方法

**A**: Constitution で言語固有の設定を行います:

```markdown
# .specify/constitution.md
## 技術スタック
- フロントエンド: Node.js + TypeScript + React
- バックエンド: Python + FastAPI
- データベース: PostgreSQL
- インフラ: Docker + Kubernetes

## 開発原則
- マイクロサービスアーキテクチャ
- API First 設計
- TDD (Test-Driven Development)
- 国際化対応 (i18n)
```

### Q4: チーム開発での運用方法

**A**: 以下のベストプラクティスを推奨:

1. **仕様書のレビュープロセス**
   - `/specify` の結果をチームでレビュー
   - 承認後に `/plan` を実行

2. **テンプレートの標準化**
   - チーム共通のテンプレートを作成
   - Git で管理・共有

3. **ナレッジの蓄積**
   - 成功例・失敗例をドキュメント化
   - Constitution の継続的改善

### Q5: 生成されるタスクが大きすぎる/小さすぎる

**A**: テンプレートで粒度を調整できます:

```markdown
# .specify/templates/tasks_template.md
## タスクの粒度
- 1タスクは 2-4時間で完了可能
- 独立してテスト可能
- コードレビューが容易な単位

## タスクフォーマット
### タスク: [機能名]
- [ ] 実装内容の詳細
- [ ] テストケースの作成
- [ ] ドキュメント更新
```

## 🔧 トラブルシューティング

### 環境関連の問題

#### Python 環境の問題

```bash
# Python バージョンが古い場合
pyenv install 3.11.7
pyenv global 3.11.7

# uv が見つからない場合
curl -LsSf https://astral.sh/uv/install.sh | sh
source ~/.bashrc
```

#### Node.js 環境の問題

```bash
# Node.js バージョンが古い場合
nvm install 18
nvm use 18

# npm の問題
npm cache clean --force
rm -rf node_modules package-lock.json
npm install
```

### Git 関連の問題

#### 認証エラー

```bash
# SSH キーの確認
ssh -T git@github.com

# Git Credential Manager の導入
# https://github.com/git-ecosystem/git-credential-manager
```

#### リポジトリアクセスの問題

```bash
# リモートリポジトリの確認
git remote -v

# プライベートリポジトリのアクセス権確認
gh auth status
```

### Spec Kit 固有の問題

#### コマンドが実行されない

```bash
# デバッグモードでの実行
uvx --from git+https://github.com/github/spec-kit.git specify init --debug

# ログの確認
cat .specify/logs/specify.log
```

#### テンプレートエラー

```bash
# テンプレートの文法確認
uvx --from git+https://github.com/github/spec-kit.git specify validate-templates

# デフォルトテンプレートの復元
uvx --from git+https://github.com/github/spec-kit.git specify reset-templates
```

### VS Code 統合の問題

#### GitHub Copilot が動作しない

1. **拡張機能の確認**
   - GitHub Copilot 拡張機能が有効
   - 最新バージョンにアップデート

2. **認証の確認**
   ```bash
   gh auth status
   ```

3. **設定の確認**
   ```json
   // .vscode/settings.json
   {
     "github.copilot.enable": {
       "*": true
     }
   }
   ```

#### カスタムコマンドが表示されない

1. **プロンプトファイルの確認**
   ```bash
   ls -la .github/prompts/
   # specify.md, plan.md, tasks.md が存在することを確認
   ```

2. **VS Code の再起動**
   - Command Palette → "Developer: Reload Window"

## 🔄 運用・保守

### 定期的なメンテナンス

#### 月次作業

```bash
# Spec Kit の更新チェック
uvx --from git+https://github.com/github/spec-kit.git specify --version

# システムヘルスチェック
uvx --from git+https://github.com/github/spec-kit.git specify check

# テンプレートの最適化
edit .specify/templates/
```

#### 四半期作業

1. **Constitution の見直し**
   - プロジェクトの進化に合わせて更新
   - 新しい技術スタックの追加

2. **ベストプラクティスの更新**
   - 成功例・失敗例の分析
   - テンプレートの改善

3. **チーム研修**
   - 新メンバーへの教育
   - 効果的な使用方法の共有

### 効果測定

#### 測定指標

```bash
# 生成されたドキュメント数
find specs/ -name "*.md" | wc -l

# 平均的な開発時間
git log --pretty=format:"%h %ad %s" --date=short | grep "feat\|fix"
```

#### 改善サイクル

1. **データ収集**: 開発時間、品質指標の測定
2. **分析**: ボトルネックの特定
3. **改善**: テンプレート・プロセスの調整
4. **検証**: 改善効果の測定

### バックアップ・復旧

#### 重要ファイルのバックアップ

```bash
# 設定ファイルのバックアップ
tar -czf spec-kit-backup.tar.gz .specify/ .github/prompts/ specs/

# Git での履歴管理
git add .specify/ .github/prompts/
git commit -m "Backup Spec Kit configuration"
```

#### 復旧手順

```bash
# 設定の復旧
tar -xzf spec-kit-backup.tar.gz

# 再初期化
uvx --from git+https://github.com/github/spec-kit.git specify check
```

### チーム運用のベストプラクティス

#### 1. 責任の明確化

- **Spec Kit 管理者**: 設定・テンプレートの保守
- **技術リーダー**: Constitution の策定・更新
- **開発者**: 日常的な使用・フィードバック

#### 2. レビュープロセス

```mermaid
graph LR
    A[要求入力] --> B[/specify実行]
    B --> C[仕様レビュー]
    C --> D{承認?}
    D -->|Yes| E[/plan実行]
    D -->|No| F[仕様修正]
    F --> C
    E --> G[計画レビュー]
    G --> H[/tasks実行]
    H --> I[実装開始]
```

#### 3. 継続的改善

- **定期的な振り返り**: 月次でプロセスの効果測定
- **テンプレート更新**: 学習内容の反映
- **ナレッジ共有**: 成功例・失敗例の共有

---

## 📞 サポート・コミュニティ

### 公式リソース

- **[GitHub Spec Kit 公式リポジトリ](https://github.com/github/spec-kit)**
- **[GitHub Copilot ドキュメント](https://docs.github.com/en/copilot)**
- **[仕様駆動開発ガイド](https://github.com/github/spec-kit/blob/main/spec-driven.md)**

### コミュニティ

- **GitHub Discussions**: [Spec Kit Community](https://github.com/github/spec-kit/discussions)
- **Stack Overflow**: `github-copilot` `spec-kit` タグ

---

**🎉 Happy Spec-Driven Development!**