# Spec Kit ファイル構造ドキュメント

## 📁 生成されたファイル構造概要

Spec Kit v0.0.30によって生成されたファイル構造を詳細に文書化します。

```
.
├── .github/prompts/          # GitHub Copilot用プロンプト (3ファイル)
└── .specify/                 # Spec Kit設定・テンプレート・スクリプト (12ファイル)
    ├── memory/               # プロジェクト憲章・コンテキスト管理 (2ファイル)
    ├── scripts/bash/         # 自動化スクリプト (6ファイル)
    └── templates/            # ドキュメントテンプレート (4ファイル)
```

## 🔧 `.github/prompts/` ディレクトリ (GitHub Copilot用)

GitHub Copilotでのカスタムコマンド用プロンプトファイル。

### ファイル一覧
- **`specify.prompt.md`** - `/specify`コマンド用プロンプト
- **`plan.prompt.md`** - `/plan`コマンド用プロンプト  
- **`tasks.prompt.md`** - `/tasks`コマンド用プロンプト

### 役割
- GitHub Copilotで `/specify`, `/plan`, `/tasks` カスタムコマンドを提供
- 仕様駆動開発のワークフローをGitHub Copilot環境で実行可能にする

## 📋 `.specify/memory/` ディレクトリ (コンテキスト管理)

プロジェクトの開発方針とコンテキスト管理。

### ファイル一覧
- **`constitution.md`** - プロジェクト憲章・開発原則
- **`constitution_update_checklist.md`** - 憲章更新チェックリスト

### 役割
- プロジェクトの不変原則・開発方針の定義
- AI エージェントが参照する一貫したガイドライン提供
- 開発チームの合意事項の文書化

## ⚙️ `.specify/scripts/bash/` ディレクトリ (自動化スクリプト)

Spec Kit操作を自動化するBashスクリプト群。

### ファイル一覧
- **`common.sh`** - 共通関数・ユーティリティ
- **`check-task-prerequisites.sh`** - タスク前提条件チェック
- **`create-new-feature.sh`** - 新機能作成スクリプト
- **`get-feature-paths.sh`** - 機能パス取得
- **`setup-plan.sh`** - 実装計画セットアップ
- **`update-agent-context.sh`** - エージェントコンテキスト更新

### 役割
- 仕様駆動開発ワークフローの自動化
- ファイル・ディレクトリ操作の標準化
- エラーハンドリングとバリデーション

## 📝 `.specify/templates/` ディレクトリ (ドキュメントテンプレート)

仕様書・計画書・タスクリスト用のMarkdownテンプレート。

### ファイル一覧
- **`spec-template.md`** - 仕様書テンプレート
- **`plan-template.md`** - 実装計画テンプレート
- **`tasks-template.md`** - タスクリストテンプレート
- **`agent-file-template.md`** - AIエージェント用テンプレート

### 役割
- 一貫したドキュメント形式の提供
- 仕様書→計画書→タスクリストの段階的作成支援
- AIエージェントによる構造化ドキュメント生成

## 🎯 GitHub Copilot統合の仕組み

### カスタムコマンドの動作フロー
1. **`/specify`** → `specify.prompt.md` → 仕様書生成 (`spec-template.md`ベース)
2. **`/plan`** → `plan.prompt.md` → 実装計画生成 (`plan-template.md`ベース)
3. **`/tasks`** → `tasks.prompt.md` → タスクリスト生成 (`tasks-template.md`ベース)

### ファイル連携
- プロンプト → スクリプト → テンプレート → 成果物ドキュメント
- `constitution.md` が全工程での一貫した指針を提供

## 🔄 ワークフロー統合

### 仕様駆動開発サイクル
```
要求 → /specify → 仕様書 → /plan → 実装計画 → /tasks → タスクリスト → 実装
```

### Node.js + Python 混在プロジェクト対応
- テンプレートは言語非依存で設計
- `constitution.md` でプロジェクト固有の技術スタック定義
- スクリプトによる環境別の自動化対応

## 📊 統計情報
- **総ファイル数**: 15個
- **総行数**: 936行
- **実行可能スクリプト**: 6個
- **テンプレート**: 4個
- **プロンプト**: 3個

この構造により、GitHub CopilotでのSpec-Driven Development が効率的に実行できます。