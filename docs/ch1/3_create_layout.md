# レイアウトを作ろう

Astroのコンポーネント指向を理解したところで、ここからは実際にそれを形にしていきましょう。

## 基本のレイアウトを作ろう

まず、　`src/layouts/default.astro` というファイルを作り、 `src/pages/index.astro` の中身をコピー&ペーストします。このとき、各ページで変える「中身」の部分は　`<slot />` にしておきましょう。

また、CSSファイルを読み込みます。今回は事前に用意しているのでそれを利用しましょう。

最終的にはこんな感じになるはずです。

```astro
---
// src/layouts/default.astro
import '../styles/global.css'
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

コミットログ: [3ed5ff6](https://github.com/s-union/astro-hands-on/commit/3ed5ff69da7dfa6eff0ea0c750ad3992d721655c)


## ヘッダーを作ろう

いよいよ実際のサイトを実装していきましょう。

### Containerコンポーネントを作ろう

まずは共通コンポーネントとして、`container.astro` というコンポーネントを作りましょう。これは幅を制限するものです。

```astro
---
// src/components/container.astro
---

<div class="container">
  <slot />
</div>


<style>
.container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 20px;
}
@media (max-width: 768px) {
  .container {
    padding: 0 10px;
  }
}
</style>
```

### Headerコンポーネントを書こう

では、実際にヘッダーとなる部分を書いていきましょう。

今回は複雑なことは書かず、サイト名とナビゲーションにとどめておきます。

```astro
---
// src/components/header.astro
import Container from "./container.astro"
---

<header>
  <Container>
    <div class="header__content">
      <span class="header__title">My Website</span>
      <nav>
        <ul>
          <li><a href="/">Home</a></li>
          <li><a href="/about">About</a></li>
          <li><a href="/contact">Contact</a></li>
        </ul>
      </nav>
    </div>
  </Container>
</header>

<style>
header {
  background-color: white;
  width: 100%;
  border-bottom: 1px solid #ccc;
}

.header__content {
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 70px;

  .header__title {
    font-size: 1.5rem;
    font-weight: bold;
  }

  ul {
    display: flex;
    list-style: none;
    margin: 0;
    padding: 0;
    gap: 20px;
  }

  a {
    text-decoration: none;
    color: black;

    &:hover {
      color: gray;
    }
  }
}
</style>
```

既にCSSについては学習しているかと思いますので詳細は説明しませんが、 `.header__title` と `nav` が両脇に配置するようになっているはずです。

これを `src/layouts/default.astro` で読み込みましょう。

```diff
---
import '../styles/global.css'

+ import Header from '../components/header.astro'
---

<html lang="ja">
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width" />
		<meta name="generator" content={Astro.generator} />
		<title>Astro</title>
	</head>
	<body>
+ 		<Header />
		<slot />
	</body>
</html>
```

こんな感じのヘッダーが確認できるはずです！

![](/docs/ch1/img/header.png)

ここまでのコミットログ: [ac7c995](https://github.com/s-union/astro-hands-on/commit/ac7c995e629858189fc5a80f1e56b4eaa3dd30b1)

## フッターを作ろう
