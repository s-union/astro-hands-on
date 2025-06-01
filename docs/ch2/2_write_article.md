# ブログ記事を書いてみよう！

ここからは実際にブログ記事を執筆してみます。[先ほどのMarkdownガイド](/docs/ch2/1_markdown.md)を参考にしながら好きなように書いてみましょう！

## Markdownファイルを作ろう

ブログ投稿のようなコンテンツをファイルのどこに置くかは特に決まっていませんが、慣例的に、 `src/contents/` 以下に置くことが多いように思えます。今回は `src/contents/blog` にファイルを置くことにしましょう。

```
.
├── src
│   ├── contents
│   │   └── blog
│   │       ├── first.md
│   │       ├── second.md
│   │       ├── ...
```

まずは拡張子が `.md` のファイルを1つ作成してみます。今回は `hello.md` とします。

こんな感じに、記事を書いてみてください。

```markdown
// src/contents/blog/hello.md
---
title: 'はじめまして！'
cover: 'image1.jpg'
created: '2025/06/01'
updated: '2025/06/01'
---

## はじめまして！

こんにちは、はじめまして！この度、新しくブログを始めることにしました。
最初の投稿として、簡単に自己紹介をさせていただきます。

...(以下省略)
```

`---` で囲まれた部分は**フロントマター**といい、このファイルの設定を示しています。以下の内容を記述してください。

- `title`: 記事のタイトル
- `cover`: 記事のサムネイル
  - 今回は事前に `src/images` 以下に画像ファイルを用意しているので、それを使用してください。
- `created`: 作成日時
- `updated`: 更新日時

同じようなMarkdownのブログ投稿を4つ作ってください！

コミットログ: [7d4f503](https://github.com/s-union/astro-hands-on/commit/7d4f5036e96dcbaa36846d668c055e08bd061258)

[次のページへ](/docs/ch2/3_content_collection.md)