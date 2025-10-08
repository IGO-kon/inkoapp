# inkoapp
🐥 インコの紹介と健康管理アプリ
🌿 概要

このアプリは、飼っているインコの情報や日々の健康状態を記録・閲覧できるシステムです。
「今日もご飯をしっかり食べたかな？」「昨日より元気そうだな」など、インコの小さな変化を記録し、
写真を眺めながら愛鳥との生活を振り返ることができます。

🧩 主な機能
カテゴリ	機能	内容
🐦 インコ管理	インコの登録・編集・削除	名前、種類、誕生日、性別、プロフィール写真などを登録
📋 健康記録	日々の体重、食事量、うんちの状態、元気度などを記録	
🍚 食事ログ	ご飯の種類・時間帯・食欲などを記録	
📸 フォトギャラリー	インコの写真をアップロードして一覧表示・拡大表示	
🧠 メモ	体調や気づいたことを自由にメモできる	
📈 統計表示	体重や食事量の推移をグラフで可視化	
🔔 リマインダー	記録忘れ防止のための通知機能（後期開発予定）	
☁️ バックアップ	クラウド同期でデータを安全に保存（Firebaseなどを利用）	
🏗️ システム構成
🔹 フロントエンド

React / Next.js

SPA構成で快適な操作性

画像プレビューやグラフ描画に対応

UIライブラリ: MUI / Tailwind CSS

グラフ描画: Chart.js または Recharts

🔹 バックエンド

Firebase（Firestore + Storage） または Supabase

データベース（ユーザー・インコ情報・記録）

画像ストレージ管理

認証機能（ログインユーザーごとにデータを管理）

🔹 データ構造（ER図）
erDiagram
    USER ||--o{ BIRD : owns
    BIRD ||--o{ HEALTH_LOG : has
    BIRD ||--o{ PHOTO : has

    USER {
        string id
        string name
        string email
    }

    BIRD {
        string id
        string user_id FK
        string name
        string species
        date birthday
        string gender
        string image_url
    }

    HEALTH_LOG {
        string id
        string bird_id FK
        date date
        float weight
        string food
        string condition
        string memo
    }

    PHOTO {
        string id
        string bird_id FK
        string image_url
        date uploaded_at
    }

🧑‍💻 開発手順
1️⃣ 環境構築
# プロジェクト作成
npx create-next-app@latest bird-health-app
cd bird-health-app

# 必要パッケージの追加
npm install firebase chart.js react-chartjs-2 tailwindcss

2️⃣ Firebase 設定

Firebase Consoleで新しいプロジェクトを作成

FirestoreとStorageを有効化

.env.local に設定を追加

NEXT_PUBLIC_FIREBASE_API_KEY=xxxxx
NEXT_PUBLIC_FIREBASE_AUTH_DOMAIN=xxxxx
NEXT_PUBLIC_FIREBASE_PROJECT_ID=xxxxx
NEXT_PUBLIC_FIREBASE_STORAGE_BUCKET=xxxxx
NEXT_PUBLIC_FIREBASE_MESSAGING_SENDER_ID=xxxxx
NEXT_PUBLIC_FIREBASE_APP_ID=xxxxx

3️⃣ ページ構成
/pages
 ├── index.tsx         # トップページ（インコ一覧）
 ├── bird/[id].tsx     # 個別ページ（健康記録・グラフ・写真）
 ├── add-bird.tsx      # 新規登録ページ
 ├── add-log.tsx       # 健康ログ記録ページ
 └── gallery.tsx       # 写真ギャラリー

4️⃣ UI 実装

インコ一覧ページ: 登録済みのインコをカード形式で表示

健康記録ページ: 日付ごとの記録と折れ線グラフ

フォトギャラリー: Storageから写真を取得して一覧表示

5️⃣ テスト & デプロイ
npm run dev   # 開発環境で確認
npm run build # 本番ビルド


デプロイ先：Vercel または Firebase Hosting

📅 今後の拡張予定

複数ユーザーによる共有（家族での閲覧）

体重・食欲の異常をAIで自動検出

インコごとのタイムライン（写真＋記録の統合）

音声メモ機能（声の記録）

🧠 想定するユーザー体験

インコの体調を日々気軽に記録できて、
写真を見返すことで「この頃少しやせてたな」と気づける。
健康記録と愛情の両立を叶えるアプリです。