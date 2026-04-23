# 実装計画 - READMEの刷新とGitHub Pagesへの公開

ツムツム非公式攻略ツール（tsumtsum-web）の README.md を刷新し、GitHub Pages で公開するための環境を整えます。

## 変更内容

### ドキュメントの刷新

#### [MODIFY] [README.md](file:///e:/Antigravity/tsumtsum-web/README.md)

- 現在の Vite テンプレートを削除し、プロジェクト専用の README に書き換えます。
- 以下の内容を含めます：
  - プロジェクト概要（ツムツム攻略ツール集）
  - 主要機能の紹介（CPM計算機、コインウォレット、スキル進捗トラッカー）
  - 技術スタック（React, TypeScript, Vite, Firebase, PWAなど）
  - デプロイ済みサイトへのリンク（GitHub Pages の URL）

### GitHub Pages 公開設定

#### [MODIFY] [vite.config.ts](file:///e:/Antigravity/tsumtsum-web/vite.config.ts)

- `base` プロパティを `'/tsumtsum-web/'` に設定します。
- PWA の `manifest` 内の `start_url` を調整します。

#### [NEW] [deploy.yml](file:///e:/Antigravity/tsumtsum-web/.github/workflows/deploy.yml)

- `main` ブランチへのプッシュ時に自動的に GitHub Pages へデプロイするワークフローを追加します。

## 検証計画

### 自動テスト

- `npm run build` を実行し、正しくビルドされることを確認します。
- `npm run lint` でエラーがないことを確認します。
- 既存のテスト `npm test` (vitest) がパスすることを確認します。

### 手動確認

- 生成された `index.html` 内の静的アセットのパスが `/tsumtsum-web/` から始まっているか確認します。
- GitHub Pages の設定手順を `walkthrough.md` に記載し、ユーザーに共有します。
