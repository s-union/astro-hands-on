# ページを作ろう

前項でページレイアウトを作ったので、ここからは実際のページを実装していきましょう。今回はまず `/about` と `/contact` を書いていきます。トップページは最後に実装します。

## aboutページを作成しよう

`src/pages/about.astro` を作成し、以下のように記述します。レイアウトを使うのを忘れずに！

```astro
---
// src/pages/about.astro
import Container from "../components/container.astro";
import Default from "../layouts/default.astro";
---

<Default>
  <Container>
    <!-- ここにページ内要素を書く -->
  </Container>
</Default>
```

### Titleコンポーネントを作ろう

ページのタイトルを表すコンポーネントを作りましょう。

`src/components/title.astro` に記述していきます。

```astro
---
// src/components/title.astro
interface Props {
  title: string;
}

const { title } = Astro.props;
---
<div class="title">
  <h1>{title}</h1>
</div>

<style>
.title {
  width: 100%;

  h1 {
    width: fit-content;
    text-align: center;
    margin: 20px auto;
    border-bottom: 3px solid #6476b6;
  }
}
</style>
```

注目すべきなのは `Props` の部分です。各コンポーネントはpropsという引数を定義し、そこに好きな値を入れることで、コンポーネントの再使用性を高めています。

ただし、どんな値でも入れてよいわけではなく、今回の場合は `title` に `string` 型のみが入るよう設定しています(ここはTypeScriptの記述方式ですね)。

### Titleコンポーネントを利用しよう

Titleコンポーネントを読み込んで、aboutページを完成させましょう。

```diff
---
import Container from "../components/container.astro";
import Default from "../layouts/default.astro";

+ import Title from "../components/title.astro";
---

<Default>
  <Container>
+     <Title title="About" />
+     <div>
+       <p>はじめまして。私の名前は理科大太郎です。</p>
+       <!-- 以下省略 -->
  </Container>
</Default>
```

コミットログ: [45e866c](https://github.com/s-union/astro-hands-on/commit/45e866cdfff831779e776691e8958dd703235ddb)

![](/docs/ch1/img/about_page.png)

お手本の中身はAIでダミーテキストを生成してもらっただけなので好きなように書いてもらって大丈夫です！

## contactページを作成しよう

次はcontactページを作ります。といっても、やることは同じなので説明は省略します！お手本のコミットログを確認しながら実装してください！

コミットログ: [569f095](https://github.com/s-union/astro-hands-on/commit/569f095d9cb5b2f07749e477d6dc88b23392368f)

# 完成！

このチャプターはここまでです！お疲れ様でした！

実際のウェブサイトのようになってきましたね。

次回はAstroのコンテンツ管理とMarkdownという記法について学んでいきましょう。

[次のページへ](/docs/ch2/1_markdown.md)