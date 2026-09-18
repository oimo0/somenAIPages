# somenAIPages

`somenAI powered by ASRO` の画面UIです。GitHub Pagesで配信し、AI処理・認証・履歴保存は自宅サーバー上の [`somenAI`](https://github.com/oimo0/somenAI) APIへHTTPSで接続します。

## GitHub Pages

リポジトリの **Settings → Pages → Build and deployment** で次を選択します。

- Source: `Deploy from a branch`
- Branch: `main`
- Folder: `/ (root)`

公開先は `https://oimo0.github.io/somenAIPages/` です。

## API接続先

`config.js` のURLを、Cloudflare TunnelなどでHTTPS公開したAPI URLへ合わせます。

```js
window.SOMENAI_API_BASE = 'https://api.somenai.asro.jp';
```

サーバー側の `.env` は次のように設定します。GitHub Pagesのパス `/somenAIPages/` はoriginに含めません。

```env
FRONTEND_ORIGIN=https://oimo0.github.io
```

ブラウザーにはログイン用トークンだけを保存します。Gemini APIキーとGroq APIキーはサーバー側だけに置き、このリポジトリには入れません。
