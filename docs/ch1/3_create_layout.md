# レイアウトを作ろう

Astroのコンポーネント指向を理解したところで、ここからは実際にそれを形にしていきましょう。

## 基本のレイアウトを作ろう

まず、　`src/layouts/default.astro` というファイルを作り、 `src/pages/index.astro` の中身をコピー&ペーストします。このとき、各ページで変える「中身」の部分は　`<slot />` にしておきましょう。

また、CSSファイルを読み込みます。今回は事前に用意しているのでそれを利用しましょう。

最終的にはこんな感じになるはずです。

```astro
src/layouts/default.astro
---
import ../styles/global.css
---

<html lang="ja">
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width" />
		<meta name="generator" content={Astro.generator} />
		<title>Astro</title>
	</head>
	<body>
		<slot />
	</body>
</html>
```

作り終わったら、　`src/pages/index.astro`　で読み込みます。読み込んだコンポーネントは通常のHTMLタグと同じように書くことができます。


## ヘッダーを作ろう

## フッターを作ろう
