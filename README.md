# Kuup AI (frontend)

`Kuup AI powered by ASRO` の画面UIです。

このフロントエンドはGitHub Pagesではなく、**ASRO側のサーバーから静的ファイルとして配信**します。AI処理・認証・履歴保存は自宅サーバー上の `somenAI` APIへHTTPSで接続します。

## 現在の構成

```
利用者
  ↓
https://asro.jp/AI/Kuup/
  ↓
ASRO側サーバー（nginxなど）
  ↓
Kuupフロントエンド
  ↓
https://somenapi.asro.jp
  ↓
somenAI API
```

GitHubリポジトリはソースコードの管理・更新に使用します。GitHubへpushしただけでは公開サイトには反映されません。

## デプロイ

Kuupのフロントエンドを実際に配信している**ASRO側のWebサーバー**で、リポジトリを更新してから静的ファイルを反映します。

例:

```bash
cd ~/somenAIPages
git pull --ff-only
```

実際の配置先が別ディレクトリの場合は、そのKuupフロントエンドの配置先で更新してください。

nginxなどでキャッシュを使用している場合は、更新後にキャッシュも確認してください。

## API接続先

`config.js` のAPI接続先は、公開APIのHTTPS URLを使用します。

```js
window.SOMENAI_API_BASE = 'https://somenapi.asro.jp';
```

サーバー側の `.env` では、実際にKuupを配信している公開Originを設定します。

```env
FRONTEND_ORIGIN=https://asro.jp
```

※ `/AI/Kuup/` のようなパスはOriginには含めません。

ブラウザーにはログイン用トークンだけを保存します。Gemini APIキーとGroq APIキーなどの秘密情報はサーバー側だけに置き、このリポジトリには入れません。

## 画面と機能

- ChatGPT風のシンプルなレスポンシブUI
- 低・中・高のモデル切り替えとモデル別残り回数
- 学習モード、Web検索（自動・常時・OFF）の設定
- Web検索・SchoolLink・計算中の状態表示と参照元カード
- Markdown表、コード、引用、簡易グラフ、生成画像の表示
- LaTeX / KaTeXによる数式表示
- Cloudflare AI画像生成モード

テーマ色は設定から5色を選択でき、端末に保存します。iPad縦画面とSplit Viewではサイドバーが引き出し式になります。VisualViewportに合わせて入力欄を配置し、画面キーボード表示時も会話部分をスクロールできます。
