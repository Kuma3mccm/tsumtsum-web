# 修正内容の確認 - READMEの刷新とGitHub Pages公開設定

tsumtsum-web の README をプロジェクト専用のものに刷新し、GitHub Pages への自動デプロイ環境を整えました。

## 実施した変更

### 1. README.md の刷新

- デフォルトの Vite テンプレートを削除し、ツムツム攻略ツールとしての概要、機能、技術スタックを記載しました。
- 各機能（CPM計算機、コインウォレット、スキル進捗管理）の解説を追加しました。
- プレミアムな印象を与えるため、各種バッジやアイコンを配置しました。

### 2. GitHub Pages 公開設定 (`vite.config.ts`)

- リポジトリ名に合わせて `base: '/tsumtsum-web/'` を設定しました。
- PWA の `start_url` を相対パス（`.`）に変更し、サブディレクトリ内でも正しく動作するように調整しました。

### 3. 自動デプロイの設定 (`.github/workflows/deploy.yml`)

- GitHub Actions を利用した自動デプロイワークフローを作成しました。
- `main` ブランチにプッシュすると、GitHub Pages へ自動的にビルド成果物が公開されます。

---

## 公開を完了するための追加手順

GitHub のリポジトリ設定で以下の操作を行ってください：

1. リポジトリの **Settings** タブを開きます。
2. 左サイドバーের **Pages** を選択します。
3. **Build and deployment** > **Source** で `GitHub Actions` を選択します。
4. `main` ブランチにこの変更をプッシュすると、自動的にデプロイが開始されます。

## 動作確認

- 設定が標準的な Vite + GitHub Pages の構成に基づいていることを確認しました。
- ローカル環境では `npm install` が必要ですが、構成ファイル（`vite.config.ts`, `deploy.yml`）が正しく配置されていることを確認済みです。
