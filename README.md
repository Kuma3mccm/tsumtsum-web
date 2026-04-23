# TSUM TSUM UTILITIES 📱

[![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-Live-brightgreen)](https://takeg.github.io/tsumtsum-web/)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![React](https://img.shields.io/badge/React-19-blue.svg)](https://reactjs.org/)
[![Vite](https://img.shields.io/badge/Vite-7-646CFF.svg)](https://vitejs.dev/)
[![TypeScript](https://img.shields.io/badge/TypeScript-5-3178C6.svg)](https://www.typescriptlang.org/)

**TSUM TSUM UTILITIES** は、LINE：ディズニー ツムツムのプレイをより楽しく、効率的にするための非公式攻略ツール集です。
PWA（Progressive Web App）に対応しており、スマートフォンにインストールしてネイティブアプリのように利用することも可能です。

---

## 🚀 主要機能

### 1. CPM Calculator (コイン効率計算)

- プレイ時間と獲得コイン数から **CPM (Coins Per Minute)** を自動計算。
- どのツムが最も効率よくコインを稼げるかを一目で把握できます。

### 2. Coin Wallet (コイン管理)

- 日々の獲得コイン数や使用コイン数をスマートに管理。
- 収支レポートを作成し、貯金目標の達成をサポートします。

### 3. Skill Progress Tracker (スキル進捗管理)

- 所有しているツムのスキルレベルと進捗を管理。
- 次のスキルアップに必要なコイン数やアイテム数を一括で確認できます。
- OCR機能（Tesseract.js）による読み取り補助も搭載。

---

## 🛠 技術スタック

- **Frontend:** React 19, Vite, TypeScript
- **State Management:** React Hooks
- **Database/Auth:** Firebase (Sync 連携)
- **Visualization:** Chart.js
- **OCR:** Tesseract.js
- **PWA:** Vite PWA Plugin
- **Styling:** Vanilla CSS (Modern CSS)

---

## 📦 インストールと実行

```bash
# リポジトリのクローン
git clone https://github.com/takeg/tsumtsum-web.git

# 依存関係のインストール
cd tsumtsum-web
npm install

# 開発サーバーの起動
npm run dev

# ビルド
npm run build
```

---

## 🌐 公開先

GitHub Pages: [https://takeg.github.io/tsumtsum-web/](https://takeg.github.io/tsumtsum-web/)

---

## 📄 ライセンス

このプロジェクトは MIT ライセンスの下で公開されています。

---

_Disclaimer: このツールはファンによる非公式のプロジェクトであり、LINE株式会社、株式会社ミクシィ、またはウォルト・ディズニー・カンパニーとは一切関係ありません。_
