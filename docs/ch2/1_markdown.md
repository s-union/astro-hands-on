# Markdownを知ろう

チャプター2へようこそ！このチャプターでは、Astroのコンテンツ管理の手法を学びます。

ですがその前に、Markdown（マークダウン）について学習していきます。

## Markdownとは？

Markdownとは、文章を記述するための軽量なマークアップ言語です。シンプルな記述で太字や斜線、見出しなどの装飾を行うことができます。MarkdownはHTMLに変換することを念頭に設計されましたが、その手軽さと汎用性の高さからWordやPowerpointなどの別のファイル形式にも変換できるようなツールも開発されています。

**このハンズオンもMarkdownで記述されています。** PreviewをCodeにするとそれが確認できます。

## Markdownの書き方

Markdownはただのプレーンテキストですので、メモ帳などでも書くことができますが、プレビュー機能のあるソフト、もしくはサイトが書くことが一般的です。

その点、VSCodeは優秀なMarkdownエディタであるといえます。シンタックスハイライトとプレビュー機能が兼ね備えているので、Markdownの記述に十分です。

![](/docs/ch2/img/markdown_preview.png)

## Markdownの記法

Markdownには様々な書き方の仕様（方言）が存在していますが、[GitHub Flavored Markdown](https://github.github.com/gfm/)というGitHubが定めた標準的な仕様がよく用いられています。今回のハンズオンでもこの仕様に沿って説明したいと思います。

### 見出し

見出しは `#` で表します。数によって、H1～H6タグに対応しています。

例:

```markdown
# 見出し1
## 見出し2
### 見出し3
#### 見出し4
##### 見出し5
###### 見出し6
```

結果:

> # 見出し1
> ## 見出し2
> ### 見出し3
> #### 見出し4
> ##### 見出し5
> ###### 見出し6

### 太字・斜体・取り消し線

例:

```markdown
*斜体*

**太字**

~~取り消し線~~
```

結果:

> *斜体*
>
> **太字**
>
> ~~取り消し線~~

### 段落

段落は改行で1行空けることで表します。pタグに対応しています。

例:

```markdown
段落1

段落2
```

結果:

> 段落1
> 
> 段落2

### 引用

`>` を使って表します。quoteタグに対応しています。

例:

```markdown
> これは引用文です。
```

結果

> これは引用文です。

### リスト

`-` を使って表します。liタグに対応しています。

例:

```markdown
- リスト1
- リスト2
- リスト3
  - サブリスト
```

結果:

> - リスト1
> - リスト2
> - リスト3
>   - サブリスト

### リンク

例:

```markdown
[Google](https://google.com)
```

結果:

> [Google](https://google.com)

### 画像

例:

```
![Astro Logo](https://astro.build/assets/press/astro-logo-dark.png)
```

結果:

> ![Astro Logo](https://astro.build/assets/press/astro-logo-dark.png)

---

これらのMarkdownはあくまでも一例です！この他にも、例えば[TeX互換の数式を扱えたり](https://docs.github.com/ja/get-started/writing-on-github/working-with-advanced-formatting/writing-mathematical-expressions)、[ハイライト付きのコードブロックを使えたり](https://docs.github.com/ja/get-started/writing-on-github/working-with-advanced-formatting/creating-and-highlighting-code-blocks)します。

参考資料をベースに調べてみることをお勧めします。

## 参考

- [MDN Web DocsのMarkdownガイド](https://developer.mozilla.org/ja/docs/MDN/Writing_guidelines/Howto/Markdown_in_MDN)
- [GitHubのMarkdownガイド](https://docs.github.com/ja/get-started/writing-on-github/getting-started-with-writing-and-formatting-on-github/basic-writing-and-formatting-syntax)

[次のページへ](/docs/ch2/2_write_article.md)