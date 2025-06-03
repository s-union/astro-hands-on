# Astroに使われている技術を知ろう

この項目ではAstroで使われている技術スタックについて紹介します。実際に個々を教えることはありませんが、自分で学習する際に必要となるものです。

## JavaScript

Webブラウザ上で動作するプログラミング言語。元々Webサイトの動きのみを扱う言語でしたが、機能が拡充するにつれ、Webサイト全般のコントロールや、ブラウザ外、つまりサーバー等にも用いられる(Node.jsなど)ようになっています。

## TypeScript

JavaScriptに静的な型をつけられるようにした言語です。

詳細は次項で説明します。

## Node.js

サーバーサイドでJavaScriptを使えるようにした実行環境です。最近ではフロントエンドの開発環境としても利用されています。

## JSX

HTMLのようにタグを書きながら、JavaScriptのロジックも一緒に書ける記法です。元々はReactというWebフレームワークのために作られました。

```jsx
function Hello(name) {
  const msg = 'Hello, ' + name;
  return (
    <h1>{msg}</h1>
  )
}
```

HTMLの書き方とJavaScriptの変数や関数を組み合わせることで、複雑なUIをもったWebページを作りやすくなります。

[次のページへ](/docs/ch0/4_javascript.md)