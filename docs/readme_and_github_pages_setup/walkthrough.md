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

## トラブルシューティング：レコードが反映されない場合

提供いただいたスクリーンショットにて、以下の警告が表示されています：

> **ⓘ カスタム ネームサーバーを使用しています**
> DNSレコードは、サードパーティーのネームサーバー プロバイダーで管理されます。

### 原因

現在、ドメインの管理（DNSレコードの参照先）が Squarespace ではなく、別のサービス（Cloudflare, Route53, Xserverなど）に設定されています。そのため、Squarespace の管理画面でいくらレコードを追加しても無視されてしまいます。

### 解決策

以下のいずれかを実施してください：

#### 案1: Squarespace のネームサーバーに戻す（推奨）

Squarespace で DNS を一括管理したい場合は、ネームサーバー設定を Squarespace 標準のものに戻します。

1. DNS設定画面の上部にある「ネームサーバー」タブ（または警告内のリンク）をクリックします。
2. 「Squarespaceネームサーバーを使用する」を選択し、保存します。
3. これにより、先ほど作成した A レコードや CNAME が有効になります。

#### 案2: 現在利用中の外部 DNS サービスで設定する

もし意図的に外部サービスを利用している場合は、**その外部サービスの管理パネル**（Squarespace ではなく）で、先に説明した 4つの A レコードと 1つの CNAME レコードを追加してください。

## Cloudflare での設定手順 (詳細)

ネームサーバーを Cloudflare に設定している場合は、Cloudflare の **DNS** メニューから以下の通り入力してください。

### 1. CNAME レコード (www 用)

- **Type:** `CNAME`
- **Name (Host):** `www`
- **Target:** `kuma3mccm.github.io`
- **Proxy status:** **DNS Only** (グレーの雲) にすることを推奨します。
  - _※Proxy (オレンジの雲) にすると GitHub 側の証明書発行やドメイン確認が失敗する場合があります。_

### 2. A レコード (ルートドメイン用)

以下の4つのレコードを追加します。

- **Type:** `A`
- **Name (Host):** `@`
- **IPv4 address:**
  - `185.199.108.153`
  - `185.199.109.153`
  - `185.199.110.153`
  - `185.199.111.153`
- **Proxy status:** **DNS Only** (グレーの雲)

---

## Git に関する注意点

- `docs` フォルダおよびその中のアイテムは、`.gitignore` 設定により GitHub にはアップロードされません。ローカル環境でのみ保持されます。

---

## ページが真っ白になる場合 (Firebase 設定エラー)

「Missing Firebase config: VITE_FIREBASE_APIKEY」というエラーが表示されてページが表示されない場合、GitHub 上で Firebase の設定値を登録する必要があります。

### 原因

Vite はビルド時に環境変数（`VITE_` で始まるもの）をコード内に埋め込みますが、GitHub Actions のビルド環境にはその値が存在しないため、エラーが発生しています。

### 解決策：GitHub Secrets への登録

以下の手順で、GitHub の管理画面に Firebase の設定値を登録してください。

1. [Firebase Console](https://console.firebase.google.com/) にアクセスし、プロジェクトを選択します。
2. 左メニュー上部の **歯車アイコン** > **プロジェクトの設定** を開きます。
3. **全般** タブの下部にある「マイアプリ」セクションで、対象のウェブアプリを確認します。
4. 「SDKの設定と構成」で **「npm を使用する」** を選択すると表示される `const firebaseConfig = { ... };` の中の値をメモします。
   - `apiKey`, `authDomain`, `projectId`, `storageBucket`, `messagingSenderId`, `appId`
5. GitHub リポジトリの **Settings** > **Secrets and variables** > **Actions** に移動します。
6. **New repository secret** ボタンを押し、以下の名称で値を一つずつ登録します：
   - **Name:** `VITE_FIREBASE_APIKEY` / **Value:** (あなたのAPIキー)
   - **Name:** `VITE_FIREBASE_AUTHDOMAIN` / **Value:** (authDomainの値)
   - **Name:** `VITE_FIREBASE_PROJECTID` / **Value:** (projectIdの値)
   - **Name:** `VITE_FIREBASE_STORAGEBUCKET` / **Value:** (storageBucketの値)
   - **Name:** `VITE_FIREBASE_MESSAGINGSENDERID` / **Value:** (messagingSenderIdの値)
   - **Name:** `VITE_FIREBASE_APPID` / **Value:** (appIdの値)

- [x] 遷移不具合（URLは変わるが画面が変わらない）の修正
  - [x] グローバルLayoutのOutletにkey（pathname）を付与
  - [x] Walletホームリンクに reloadDocument を付与

---

## クラウド保存時に「ERR_BLOCKED_BY_CLIENT」エラーが出る場合

このエラーは、ブラウザの拡張機能（広告ブロックなど）が Firebase (Firestore) への通信を「広告や追跡」と誤認してブロックしている場合に発生します。

### 解決策1：広告ブロック拡張機能をオフにする

- **AdBlock**, **uBlock Origin**, **Privacy Badger** などの拡張機能を使用している場合、`www.kuma3mccm.com` でこれらを無効（一時停止）にしてください。
- ウイルス対策ソフト（Kaspersky, Norton 等）の「Web保護」機能がブロックしている場合もあります。

### 解決策2：Firebase コンソールで Firestore を作成する

1. [Firebase Console](https://console.firebase.google.com/) > **Firestore Database** を開きます。
2. もしまだ作成していない場合は **「データベースの作成」** をクリックして作成してください。
3. ロケーションを選択（例: `asia-northeast1`）し、最初は「テストモード」または「本番環境モード」で開始します。

### 解決策3：セキュリティルールの確認

1. Firestore の **「ルール」** タブを開きます。
2. 以下のように、ログイン済みユーザーのみが自分のデータを読み書きできるように設定されているか確認してください：
   ```javascript
   rules_version = '2';
   service cloud.firestore {
     match /databases/{database}/documents {
       match /users/{userId} {
         allow read, write: if request.auth != null && request.auth.uid == userId;
       }
       // またはテスト用に一時的に全員許可する場合 (本番公開時は上記推奨)
       // match /{document=**} {
       //   allow read, write: if request.auth != null;
       // }
     }
   }
   ```

---

## スキルページの OCR (一括入力) の使い方

「スキル」ページでは、ゲーム画面のスクリーンショットをアップロードすることで、ツムの所持数を自動でカウントできます。

### 基本的な手順

1. ゲーム内の「ツム一覧」または「スキルレベル確認」のスクリーンショットを複数枚撮影します。
2. アプリの「スキル」ページにある **「スクショOCR一括入力」** セクションへ移動します。
3. **「画像をアップロード」** ボタンを押し、撮影した画像を選択します。
4. OCR処理が開始されます。結果が表示されるまで数秒〜数十秒待ちます。
5. 解析結果が表示されるので、正しくツムが認識されているか確認します。
   - もし認識が間違っている場合は、候補ボタンから正しいツムを選び直せます。
6. 全て確認できたら **「確定して所持数に +1」** ボタンを押します。これで各ツムの所持数が更新されます。

### 精度を上げるコツ

- **トリミング調整**: 画面上下左右の不要な部分（レベルゲージやボタンなど）を削る設定を調整できます。ツムの名前だけが綺麗に残るように設定すると精度が上がります。
- **画像の向き**: スクリーンショットは必ず垂直（回転していない状態）でアップロードしてください。

### OCRログでエラー (404) が出る場合

`Network error while fetching ... jpn.traineddata.gz. Response code: 404` というエラーが出ていた問題は、参照先のデータサーバー（CDN）のパスが変更されていたことが原因です。
現在はより安定した `https://tessdata.projectnaptha.com/4.0.0_best` を参照するように修正済みです。

---

## ログイン時に「auth/configuration-not-found」エラーが出る場合

このエラーは、Firebase 側で認証機能が有効になっていないか、カスタムドメインが許可されていない場合に発生します。

### 解決策1：認証機能を有効にする

1. [Firebase Console](https://console.firebase.google.com/) の左メニューから **Authentication** を選択します。
2. 初めての場合は **「始める」** をクリックします。
3. **Sign-in method** タブを開き、**Google** をクリックして「有効」に設定し、保存します。

### 解決策2：承認済みドメインにカスタムドメインを追加する

1. Authentication 画面の **Settings** タブを開きます。
2. 左メニューの **Authorized domains** (承認済みドメイン) を選択します。
3. **「ドメインを追加」** をクリックして、以下のドメインを追加してください：
   - `www.kuma3mccm.com`
   - `kuma3mccm.github.io` (まだなければ)
4. これで、カスタムドメインからのログインが許可されます。

---

## 動作確認ツール

設定が反映されているか、以下のサイトで確認できます：

- [whatsmydns.net](https://www.whatsmydns.net/#A/www.kuma3mccm.com) (AレコードやCNAMEが正しく引けているか世界中からチェックできます)
