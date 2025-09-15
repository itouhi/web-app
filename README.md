# Web Application with Spec Kit

> **GitHub Copilot 駆動の仕様駆動開発 (Spec-Driven Development) プロジェクト**

このプロジェクトは、[GitHub Spec Kit](https://github.com/github/spec-kit) を活用した仕様駆動開発のベストプラクティスを実装したWebアプリケーション開発環境です。GitHub Copilot との統合により、要求分析から実装まで一貫したワークフローを提供します。

## 🚀 クイックスタート

### 前提条件

- **GitHub Copilot (VS Code)** - 必須
- **Python 3.11+** (推奨: 3.13+)
- **uv** (Pythonパッケージマネージャー) v0.8.17+
- **Node.js 18+** (TypeScript開発用)
- **Git**
- **Linux/macOS** または WSL2 on Windows

### 5分でセットアップ

```bash
# 1. リポジトリをクローン
git clone https://github.com/itouhi/web-app.git
cd web-app

# 2. Spec Kit が既にインストール済みか確認
uvx --from git+https://github.com/github/spec-kit.git specify check

# 3. VS Code で開く
code .

# 4. GitHub Copilot コマンドを試す
# VS Code で Ctrl+Shift+P → "GitHub Copilot: /specify" を実行
```

## 🛠️ 主な機能

### GitHub Copilot カスタムコマンド

| コマンド | 用途 | 例 |
|---------|------|-----|
| `/specify` | 要求から仕様作成 | ユーザー認証システムを仕様化 |
| `/plan` | 仕様から実装計画 | 認証システムの実装ステップ生成 |
| `/tasks` | 計画から実装タスク | 具体的なコーディングタスク作成 |

### 開発フロー

```mermaid
graph LR
    A[要求] --> B["/specify<br/>仕様作成"]
    B --> C["/plan<br/>実装計画"]
    C --> D["/tasks<br/>実装タスク"]
    D --> E["実装<br/>(GitHub Copilot)"]
    E --> F[レビュー]
    F --> G[デプロイ]
```

## 📁 プロジェクト構造

```
├── README.md                     # このファイル
├── docs/                         # ドキュメント
│   ├── spec-kit-guide.md        # Spec Kit 詳細ガイド
│   ├── development-process.md    # 開発プロセス詳細
│   ├── command-reference.md      # コマンドリファレンス
│   ├── spec-kit-best-practices.md # ベストプラクティス集
│   ├── team-guidelines.md       # チーム開発ガイドライン
│   └── github-copilot-workflow-validation.md # ワークフロー検証結果
├── .specify/                     # Spec Kit設定
│   ├── constitution.md          # プロジェクト憲法
│   ├── templates/               # テンプレート
│   └── scripts/                 # 自動化スクリプト
├── .github/prompts/             # GitHub Copilot プロンプト
├── specs/                       # 仕様書ディレクトリ
└── .vscode/                     # VS Code設定
    └── spec-kit-settings.md     # VS Code統合設定説明
```

## 📚 ドキュメント

### 基本ガイド
- **[Spec Kit 導入・運用ガイド](docs/spec-kit-guide.md)** - 詳細なセットアップと使用方法
- **[開発プロセス](docs/development-process.md)** - 仕様駆動開発のワークフロー
- **[コマンドリファレンス](docs/command-reference.md)** - `/specify`, `/plan`, `/tasks` の詳細

### ベストプラクティス
- **[ベストプラクティス集](docs/spec-kit-best-practices.md)** - 効果的な開発手法
- **[チーム開発ガイドライン](docs/team-guidelines.md)** - 複数人での開発方法
- **[GitHub Copilot ワークフロー検証](docs/github-copilot-workflow-validation.md)** - 実証結果

### VS Code 統合
- **[VS Code 統合設定](/.vscode/spec-kit-settings.md)** - エディター最適化

## 🎯 使用例

### 新機能の開発

```bash
# 1. 要求を仕様に変換
# VS Code で `/specify` コマンドを実行
"ユーザーがプロフィール画像をアップロードできる機能を追加したい"

# 2. 仕様から実装計画を作成
# 生成された spec.md を元に `/plan` コマンドを実行

# 3. 実装タスクを生成
# 生成された plan.md を元に `/tasks` コマンドを実行

# 4. タスクを実装
# GitHub Copilot を使って各タスクを実装
```

### バグ修正・改善

```bash
# 既存仕様の更新
# `/specify` で現在の仕様を更新

# 修正計画の作成
# `/plan` で修正手順を計画

# 実装タスクの生成
# `/tasks` で具体的な修正タスクを作成
```

## 🛡️ 品質保証

### 自動検証
- **Constitution Check**: プロジェクト憲法との整合性検証
- **Template Validation**: テンプレート形式の検証
- **TDD Integration**: テスト駆動開発の強制

### 継続的改善
- **定期的な振り返り**: 開発効率の測定と改善
- **テンプレート更新**: 学習内容の反映
- **プロセス最適化**: ワークフローの継続的改善

## 🏢 チーム開発

### レビュープロセス
1. **仕様レビュー**: `/specify` の結果をチームで確認
2. **計画レビュー**: `/plan` の結果をアーキテクトが確認
3. **実装レビュー**: 通常のコードレビューを実施

### ナレッジ共有
- **仕様書の共有**: `specs/` ディレクトリで管理
- **学習内容の蓄積**: ベストプラクティスの更新
- **経験の共有**: チームガイドラインの改善

## 🔧 トラブルシューティング

### よくある問題

#### GitHub Copilot コマンドが認識されない
```bash
# Spec Kit の再初期化
uvx --from git+https://github.com/github/spec-kit.git specify init --here --ai copilot

# VS Code の再起動
```

#### Python/Node.js 環境の問題
```bash
# Python環境の確認
python --version  # 3.11+ が必要
uv --version      # v0.8.17+ が必要

# Node.js環境の確認
node --version    # 18+ が必要
npm --version
```

#### Git認証の問題
```bash
# Git Credential Manager の導入を検討
# https://github.com/git-ecosystem/git-credential-manager
```

詳細は [トラブルシューティングガイド](docs/spec-kit-guide.md#troubleshooting) を参照してください。

## 📊 効果測定

### 導入効果の実証結果
- **開発効率**: 要求→実装の時間を **数日から数時間** に短縮
- **ドキュメント生成**: **372行** の実用的ドキュメントを自動生成
- **タスク管理**: **44個** の具体的実装タスクを自動生成
- **品質向上**: TDD強制、Constitution Check による品質保証

### 測定指標
- **開発速度**: 機能追加にかかる時間
- **コード品質**: テストカバレッジ、複雑度
- **チーム満足度**: 開発体験の向上度

## 🌟 技術スタック

### 支援言語・フレームワーク
- **Node.js + TypeScript**: フロントエンド・バックエンド
- **Python 3.13**: データ処理・AI統合
- **混在プロジェクト**: マイクロサービス対応

### 開発環境
- **VS Code + GitHub Copilot**: メイン開発環境
- **Dev Container**: 一貫した開発環境
- **GitHub Actions**: CI/CD パイプライン

## 🤝 コントリビューション

1. **Issue作成**: 機能要求・バグ報告
2. **仕様駆動開発**: `/specify` での仕様作成から開始
3. **プルリクエスト**: レビューを経て本番反映
4. **ドキュメント更新**: 学習内容の共有

詳細は [チーム開発ガイドライン](docs/team-guidelines.md) を参照してください。

## 📄 ライセンス

このプロジェクトは MIT ライセンスの下で公開されています。

## 🔗 関連リンク

- **[GitHub Spec Kit 公式](https://github.com/github/spec-kit)**
- **[GitHub Copilot ドキュメント](https://docs.github.com/en/copilot)**
- **[仕様駆動開発ベストプラクティス](https://github.com/github/spec-kit/blob/main/spec-driven.md)**

---

**🎉 Happy Spec-Driven Development with GitHub Copilot!**
