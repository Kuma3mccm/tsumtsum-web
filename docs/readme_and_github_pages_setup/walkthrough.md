# 修正内容の確認 - READMEの刷新とGitHub Pages公開設定

tsumtsum-web の README をプロジェクト専用のものに刷新し、GitHub Pages への自動デプロイ環境を整えました。

## 実施した変更

### 1. README.md の刷新

- デフォルトの Vite テンプレートを削除し、ツムツム攻略ツールとしての概要、機能、技術スタックを記載しました。
- 各機能（CPM計算機、コインウォレット、スキル進捗管理）の解説を追加しました。
- プレミアムな印象を与えるため、各種バッジやアイコンを配置しました。

### 2. カスタムドメイン対応 (`www.kuma3mccm.com`)

- `vite.config.ts` の `base` パスを `'/'`（ルート）に設定しました。
- `public/CNAME` ファイルを作成し、ドメイン名を記述しました。
- `README.md` 内の公開 URL を新ドメインに更新しました。

### 3. 自動デプロイの設定 (`.github/workflows/deploy.yml`)

- GitHub Actions を利用した自動デプロイワークフローを作成済みです。
- `main` ブランチにプッシュすると、新ドメインへ自動的にデプロイされます。

---

## 公開を完了するための追加手順

GitHub およびドメイン管理サービスで以下の設定を行ってください：

1. **GitHub Pages のドメイン設定**:
   - リポジトリの **Settings** > **Pages** で **Custom domain** に `www.kuma3mccm.com` を入力して保存します。
   - **Enforce HTTPS** にチェックを入れることを推奨します。

## Squarespace でのドメイン設定手順 (詳細)

CNAMEの設定がうまくいかない場合、以下の設定を一つずつ確認してください。

### 1. Squarespace DNS設定画面を開く

- Squarespace にログインし、[Domains](https://account.squarespace.com/domains) パネルを開きます。
- 設定するドメインを選択し、**DNS Settings** をクリックします。

### 2. 不要なレコードの削除

- **重要:** すでにある CNAME や A レコードの中で、Squarespace デフォルトのものがあれば削除（または編集）して競合を防ぎます。特に `www` ホストのレコードが既にある場合は、古いものを削除してください。

### 3. CNAME レコードの追加 (www 用)

- **Host:** `www`
- **Type:** `CNAME`
- **Data (Points to):** `kuma3mccm.github.io`
- **TTL:** デフォルト（3600など）でOK

### 4. A レコードの追加 (ルートドメイン用)

GitHub Pages ではルートドメイン（`@`）に対して以下の4つの IP アドレスを設定することを推奨しています。

- **Host:** `@` (または空欄)
- **Type:** `A`
- **Data:** - `185.199.108.153` - `185.199.109.153` - `185.199.110.153` - `185.199.111.153`
  （それぞれ新しい A レコードとして追加してください）

### 5. GitHub 側の設定確認

- リポジトリの **Settings** > **Pages** > **Custom domain** に `www.kuma3mccm.com` が入力されていることを確認。
- **Save** を押した後、"DNS check successful" と表示されるまで待ちます（反映には数分〜最大72時間かかることがあります）。

---

## 動作確認ツール

設定が反映されているか、以下のサイトで確認できます：

- [whatsmydns.net](https://www.whatsmydns.net/#A/www.kuma3mccm.com) (AレコードやCNAMEが正しく引けているか世界中からチェックできます)
