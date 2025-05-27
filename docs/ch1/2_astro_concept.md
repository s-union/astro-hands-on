# Astroの考え方

Astroは他のフロントエンドフレームワーク(具体的にはReactやNext.jsなどの新進気鋭なライブラリたち)の影響を受けているので、考え方もよく似ています。一緒に見てみましょう。

## .astroファイルの見方

```astro
---
// ここにJavaScriptのコード部が入る
const msg = 'Hello World'
---

<!-- ここにHTMLのコード部が入る -->
<div>{ msg }</div> <!-- <div>Hello World</div> -->

<style>
/* ここにCSSのコード部が入る */
div {
  font-size: 2rem
}
</style>
```

AstroはJavaScript(TypeScript)、HTML、CSSを1つのファイル上で記述します。

## Astroのディレクトリ構造

Astroは以下のような構造になっています。

![](/docs/ch1/img/astro_directory.png)

- `pulic/`: faviconなど、コピーするだけのファイルはここに入れます。
- `src/`: Astroのファイル類はこのsrc以下に入れる、ということになっています。
  - `components/` : コンポーネント(後述)を入れます。
  - `images/`: 画像ファイルをここに格納します。
  - `layouts`: レイアウト(後述)を入れます。
  - `pages/`: ルーティングに関与します(後述)。
  - `styles`: CSSファイルなどをここに格納します。
- `astro.config.{mjs|ts}`: Astro本体の設定をします。

### `src/pages/` について

`src/pages/` 以下の.astroファイルは **ルーティング** と呼ばれる、URLのパスと処理の紐づけ作業に関与します。

例を見てみましょう。こんなファイル構造があるとします。

```
/
└─ src
   └─ pages
      ├─ posts
      │     ├─ special.astro
      │     └─ [id].astro
      ├─ about.astro
      └─ index.astro
```

この場合、Astroは以下のルーティングを用意します。

- `src/pages/index.astro` -> `/`
- `src/pages/about.astro` -> `/about`
- `src/pages/posts/special.astro` -> `/posts/special`
- `src/pages/posts/[id].astro` -> `/posts/*`
  - `/posts/` 以下の全て

このようなファイルの構造からルーティングを決定することを **ファイルベースルーティング** (File-based Routing)といいます。

## コンポーネント指向

Astroをはじめ現代のフロントエンドは **コンポーネント指向** の考え方が主流です。では、そもそもコンポーネントとは一体なんでしょうか？

Webサイトを見ていると、同じようなものが使い回されていることに気づきます。

![](/docs/ch1/img/amazon-component.png)

例えばAmazonの商品ページでは、個々の商品は同じようなパーツの使い回しで表示されていたり(赤色)、ヘッダーのように常にどのページでも同じように表示されていたり(青色)するわけです。

コンポーネント指向の核はこの使い回しです。