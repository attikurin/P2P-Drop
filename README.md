<div align="center">

# ⚡ P2P Drop

### サーバーを経由しない、ブラウザ間直接ファイル共有

**WebRTC を利用した完全 P2P・サーバーレスの一時ファイル共有アプリ**

![HTML5](https://img.shields.io/badge/HTML5-E34F26?style=flat&logo=html5&logoColor=white)
![JavaScript](https://img.shields.io/badge/JavaScript-F7DF1E?style=flat&logo=javascript&logoColor=black)
![TailwindCSS](https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=flat&logo=tailwind-css&logoColor=white)
![WebRTC](https://img.shields.io/badge/WebRTC-333333?style=flat&logo=webrtc&logoColor=white)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

</div>

---

## 📖 概要

**P2P Drop** は、ブラウザ間で直接ファイルを送受信するためのサーバーレスな一時ファイル共有アプリケーションです。

WebRTC 技術（PeerJS）を利用しており、**ファイルが外部のクラウドサーバー等に保存されることはありません**。送信者のデバイスから受信者のデバイスへ直接転送されるため、高いプライバシーを保ったままファイル共有ができます。

たった1つの HTML ファイルで動作する、シンプルで強力な「使い捨て共有」ツールです。

---

## ✨ 特徴

### 🔒 プライバシー重視
- **完全な P2P 通信**: ファイルは送信者のデバイスから受信者のデバイスへ直接転送
- **自動消去（有効期限）機能**: 5分〜3時間の任意の時間で自動的に通信を遮断し、ブラウザのメモリからファイル参照を破棄
- **タブを閉じれば即停止**: 送信者がタブを閉じた瞬間に共有も停止

### 🚀 使いやすさ
- **QRコード対応**: 共有 URL を QR コードで表示。スマホでスキャンするだけで受信可能
- **複数ファイル対応**: 複数のファイルを選択すると自動的に ZIP に圧縮して送信
- **ドラッグ&ドロップ**: ファイル選択も直感的
- **動画・大容量対応**: チャンク化（64KB単位）でメモリ効率よく転送、受信後にプレビュー再生も可能

### 📊 視認性の高い UX
- **リアルタイム進捗表示**: 送信・受信ともに進捗バー、転送速度（MB/s）、残り時間（ETA）を表示
- **トースト通知**: アラートでブロックされない、洗練された通知 UI
- **自動消去カウントダウン**: 残り時間を秒単位で常時表示
- **モバイル離脱対策**: Screen Wake Lock API でスマホの画面ロックを自動抑止

### 🧩 シンプル構成
- **1つの HTML ファイル**だけで完結
- バックエンド構築不要
- ※ P2P 通信の確立には PeerJS の公開シグナリングサーバーを利用

---

## 🚀 使い方

### 📤 送信者（ファイルを渡す側）

1. 本アプリ（`index.html`）をブラウザで開きます
2. 共有したいファイルを**ドラッグ&ドロップ**、または**クリックして選択**します
   - 複数のファイルも一括選択可能（自動で ZIP にまとめられます）
3. **自動消去までの時間（有効期限）** を選択します（5分〜3時間）
4. **「共有リンクを作成」** ボタンをクリック
5. 生成された **QR コード** または **URL** を受信者に送信
   - スマホ受信なら QR スキャンが最速
   - 「コピー」ボタンで URL をクリップボードへ一発コピー

> ⚠️ **重要**: 受信者がファイルのダウンロードを完了するまで、絶対にこのタブを閉じないでください。タブを閉じると通信が切断され、共有が即座に停止します。

### 📥 受信者（ファイルを受け取る側）

1. 送信者から送られてきた共有リンクをブラウザで開く（または QR コードをスキャン）
2. 自動的に送信者と接続され、ファイルの受信が開始されます
3. プログレスバーが 100% になり、「受信完了！」と表示されるまでそのまま待ちます
   - 進捗・速度・残り時間がリアルタイム表示されます
4. プレビューを確認し、**「デバイスに保存」** ボタンをクリックしてファイルを保存

---

## 🖼 画面遷移

```
[送信側]
  ファイル選択画面
    ├─ ドラッグ&ドロップ / クリック選択
    ├─ ファイル一覧（複数可、個別削除可）
    └─ 有効期限選択
        ↓
  (複数選択時) ZIP圧縮画面
    └─ 圧縮プログレス表示
        ↓
  共有中画面
    ├─ QRコード（180/200px）
    ├─ 共有URL + コピーボタン
    ├─ 接続状態インジケーター
    ├─ 送信進捗バー（接続後）
    └─ 自動消去カウントダウン

[受信側]
  受信中画面
    ├─ 進捗バー
    ├─ 転送速度（MB/s）
    └─ 残り時間（ETA）
        ↓
  受信完了画面
    ├─ ファイル情報
    ├─ プレビュー（動画/画像/音声/ZIP）
    └─ ダウンロードボタン
```

---

## ⚠️ 動作環境とホスティングについて

このアプリは URL パラメータ（`?peer=...`）を利用して通信相手を特定します。そのため、HTML ファイルを直接ダブルクリックして開いた状態（URL が `file:///...` の状態）では、**別の端末からアクセスできる共有リンクを生成できません**。

別のスマホや PC と共有したい場合は、以下のいずれかの方法でアプリをご利用ください。

### ✅ 方法1: Web ホスティングサービスを利用する（推奨）

GitHub Pages、Vercel、Netlify、Cloudflare Pages などの無料静的ホスティングサービスに `index.html` をアップロードして公開します。これが最も確実で簡単な方法です。

<details>
<summary><b>📘 GitHub Pages での公開手順</b></summary>

1. GitHub で新しいリポジトリを作成
2. `index.html` をアップロード
3. リポジトリの **Settings → Pages** へ移動
4. **Source** を `Deploy from a branch` に設定
5. **Branch** を `main` (root) に選択して **Save**
6. 数分後、`https://<username>.github.io/<repo>/` でアクセス可能に

</details>

<details>
<summary><b>📗 Vercel / Netlify での公開手順</b></summary>

1. [Vercel](https://vercel.com/) または [Netlify](https://www.netlify.com/) にサインアップ
2. 「New Project」または「Import from Git」を選択
3. `index.html` を含むリポジトリを選択（または `index.html` をドラッグ&ドロップでデプロイ）
4. デプロイ完了後、発行された HTTPS URL でアクセス

</details>

### ✅ 方法2: ローカルサーバーを利用する（同一ネットワーク内のみ）

送信者と受信者が同じ Wi-Fi（LAN）に接続している場合は、ローカルサーバーを立ち上げてアクセスします。

```bash
# Python の場合
python -m http.server 8000

# Node.js の場合
npx serve .

# PHP の場合
php -S 0.0.0.0:8000
```

その後、`http://<あなたのローカルIPアドレス>:8000/` で別端末からアクセス。

> 💡 **Tips**: VS Code 拡張機能「Live Server」を使うと、ファイル編集と同時にローカルサーバーが起動するので便利です。

---

## 🛑 制限事項

| 項目 | 内容 |
|------|------|
| **メモリ使用量** | 受信側はブラウザの RAM 上でファイルを結合します。数 GB に及ぶ極端に巨大なファイルを受信すると、特にスマートフォンのブラウザがクラッシュする可能性があります |
| **同時受信者** | 想定は1対1。複数の受信者が同時に接続する場合の挙動は最適化されていません |
| **同一ブラウザ** | 送受信中はブラウザのタブを閉じないでください |
| **NAT 越え** | 法人ネットワークなどの厳しい NAT 環境では P2P 直結に失敗する場合があります（将来的に TURN サーバー対応予定） |

一時的な動画やドキュメントの共有用途を想定しています。

---

## 🛠 使用技術

| 技術 | 用途 |
|------|------|
| **HTML5 / JavaScript / CSS** | ベース |
| **[Tailwind CSS](https://tailwindcss.com/)** (CDN) | スタイリング |
| **[PeerJS](https://peerjs.com/) v1.5.2** | WebRTC P2P 通信ライブラリ |
| **[JSZip](https://stuk.github.io/jszip/) v3.10.1** | 複数ファイルの ZIP 圧縮 |
| **[QRCode.js](https://github.com/davidshimjs/qrcodejs)** | QR コード生成 |
| **[Lucide Icons](https://lucide.dev/)** | アイコンセット |
| **[Screen Wake Lock API](https://developer.mozilla.org/docs/Web/API/Screen_Wake_Lock_API)** | モバイル端末の画面ロック抑止 |
| **[Clipboard API](https://developer.mozilla.org/docs/Web/API/Clipboard_API)** | URL のワンクリックコピー |

---

## 🌐 ブラウザ対応

| ブラウザ | 送信 | 受信 | 備考 |
|---------|------|------|------|
| Chrome / Edge (最新) | ✅ | ✅ | 全機能対応 |
| Firefox (最新) | ✅ | ✅ | 全機能対応 |
| Safari (iOS 14.5+ / macOS 11+) | ✅ | ✅ | Wake Lock は iOS 16.4+ で対応 |
| Android Chrome | ✅ | ✅ | 全機能対応 |
| IE | ❌ | ❌ | 非対応 |

> 💡 HTTPS 環境での利用を推奨します（Clipboard API は HTTPS でのみ動作。HTTP の場合は自動でフォールバック処理）

---

## 📂 プロジェクト構成

```
p2p-drop/
└── index.html   ← これだけ！すべてが詰まっています
```

たった1ファイルで完結します。ビルドツールも依存関係インストールも不要です。

---

## 🤝 コントリビュート

バグ報告、機能リクエスト、Pull Request は大歓迎です！

1. このリポジトリをフォーク
2. フィーチャーブランチを作成 (`git checkout -b feature/amazing-feature`)
3. 変更をコミット (`git commit -m 'Add some amazing feature'`)
4. ブランチへプッシュ (`git push origin feature/amazing-feature`)
5. Pull Request を作成

---

## 🛣 ロードマップ

将来的に検討している改良案：

- [ ] **エンドツーエンド暗号化（E2EE）**: URL ハッシュに AES-GCM 鍵を埋め込む方式
- [ ] **StreamSaver による逐次保存**: 数 GB 超のファイルもメモリ不足にならない
- [ ] **SHA-256 整合性検証**: 受信後にハッシュ照合で破損検知
- [ ] **TURN サーバー対応**: 厳しい NAT 環境でも接続成功率向上
- [ ] **PWA 化**: ホーム画面追加・オフライン起動対応
- [ ] **再接続・再開機能**: 通信断時に続きから再開
- [ ] **双方向送信**: 受信側からも送信できるチャット風 UI
- [ ] **自前シグナリングサーバー対応**: PeerServer のセルフホスト手順

---

## ❓ FAQ

<details>
<summary><b>Q. 本当にサーバーにファイルは保存されないの？</b></summary>

A. はい。ファイルデータは送信者→受信者へ直接 WebRTC で転送されます。ただし、P2P 接続を確立するための「シグナリング」処理だけは PeerJS の公開サーバーを経由します。シグナリングサーバーは接続情報（IP アドレスなど）の橋渡しをするのみで、ファイル本体は通りません。

</details>

<details>
<summary><b>Q. 通信は暗号化されている？</b></summary>

A. はい。WebRTC の通信は DTLS で自動的に暗号化されています。ただし、シグナリングサーバーには接続メタデータが渡るため、完全な E2EE が必要な場合はロードマップにある AES-GCM ベースの追加暗号化を待つか、自前シグナリングサーバーをご利用ください。

</details>

<details>
<summary><b>Q. ファイルサイズの上限は？</b></summary>

A. 明示的な上限はありませんが、**受信側のメモリ容量**に依存します。目安として：
- PC（メモリ 8GB+）: 2〜4 GB まで快適
- スマホ: 数百 MB〜1 GB が安全圏

将来的に StreamSaver 対応すれば、この制限は解消される予定です。

</details>

<details>
<summary><b>Q. 受信者が複数いる場合は？</b></summary>

A. 現状は1対1での共有を想定しています。複数の受信者に同じファイルを送りたい場合は、各受信者ごとに別々の共有リンクを生成してください。

</details>

<details>
<summary><b>Q. スマホで送信中、画面ロックされても大丈夫？</b></summary>

A. Screen Wake Lock API により、共有中は自動的に画面ロックが抑止されます。ただし iOS は 16.4 以降の対応です。古い iOS の場合は、設定で「自動ロック」を「なし」に変更することをおすすめします。

</details>

<details>
<summary><b>Q. なぜタブを閉じると共有が止まる？</b></summary>

A. ファイルはあなたのブラウザのメモリに保持されており、WebRTC 接続もあなたのブラウザが終端しています。タブを閉じると両方が失われるため、共有が継続できなくなります。これはサーバーレスである代償でもあり、プライバシー上のメリットでもあります。

</details>

---

## 📝 ライセンス

MIT License — 商用・非商用問わず自由にご利用ください。

```
Copyright (c) 2026 P2P Drop Contributors

Permission is hereby granted, free of charge, to any person obtaining a copy
of this software and associated documentation files (the "Software"), to deal
in the Software without restriction...
```

---

## 🙏 謝辞

このプロジェクトは以下のオープンソースプロジェクトのおかげで成り立っています：

- [PeerJS](https://peerjs.com/) — WebRTC 抽象化レイヤー
- [Tailwind CSS](https://tailwindcss.com/) — ユーティリティファースト CSS
- [JSZip](https://stuk.github.io/jszip/) — ブラウザ内 ZIP 生成
- [Lucide](https://lucide.dev/) — 美しいアイコンセット
- [QRCode.js](https://github.com/davidshimjs/qrcodejs) — シンプルな QR 生成

---

<div align="center">

### ⚡ Made with WebRTC, for true privacy. ⚡

**[🌟 Star on GitHub](#) ・ [🐛 Report Issues](#) ・ [💡 Suggest Features](#)**

</div>
