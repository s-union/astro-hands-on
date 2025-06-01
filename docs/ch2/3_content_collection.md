# コンテンツ管理をしよう

Astroではコンテンツ管理を行うための機能が備わっています。今回はこれを利用して、ブログ記事を型安全に取り出す方法を学びます。

> [!IMPORTANT]
> 今回の内容はTypeScriptをある程度理解している人向けですので、全てを理解する必要はありません。難しいと感じたらコピペでも大丈夫です。

## コンテンツ管理の設定をしよう

Astroにはコンテンツコレクションという機能があります。コンテンツコレクションは `src/content.config.ts` で指定します。

> [!NOTE]
> AstroのコンテンツコレクションはVer 5.0からと比較的新しい機能です。古い情報と相違のある点がありますので注意してください。

```typescript
import { glob } from 'astro/loaders';
import { defineCollection, z } from 'astro:content';

const blog = defineCollection({
  // 'src/contents/blog'内のMarkdownファイルを読み込む
  loader: glob({ base: './src/contents/blog', pattern: '**/*.md' }),

  // Markdownのスキーマを定義
  schema: z.object({
    title: z.string(),
    cover: z.string(),
    created: z.string(),
    updated: z.string().optional(),
  }),
});

export const collections = { blog };
```

### 解説

Astroには `defineCollection` という関数を定義し、それをエクスポートすることで、外部から型安全にコンテンツを参照する仕組みがあります。

<details>
<summary>より詳細な解説(TypeScriptに慣れている人向け)</summary>

`defineCollection` では `loader` と `schema` という2つの値を定義する必要があります。

#### loader

コンテンツを読み込む方式を定義します。今回の場合、 `glob` という関数を用いて `src/contents/blog` 以下の拡張子 `.md` のファイルを読み込むように指定しています。

#### schema

スキーマという、loaderで読み込んだデータのデータ構造(今回の場合Markdownのフロントマター)を定義し、読み込み時にそのデータ構造と一致しているかをチェックします。

[Zod](https://zod.dev) というライブラリが元になっており、こうすることで予期しないデータ構造にエラーを出したり、コンテンツを読み込む際に型安全にオプションを使うことができます。

今回の場合は以下のような型定義と同義になります。

```typescript
type MarkdownSchema = {
  title: string;
  cover: string;
  created: string;
  updated?: string;
};
```

</details>

## コンテンツを読み込もう

`src/pages/blog/[...id].astro` というファイルを作り、以下のように書いてください。

```astro
---
// src/pages/blog/[...id].astro
import { getCollection, render, type CollectionEntry } from 'astro:content';
import Container from '../../components/container.astro';
import Default from '../../layouts/default.astro';

export async function getStaticPaths() {
  const blogEntries = await getCollection('blog');
  return blogEntries.map((entry) => ({
    params: { id: entry.id },
    props: { entry },
  }));
}

interface Props {
  entry: CollectionEntry<'blog'>;
}

const { entry } = Astro.props;
const { Content } = await render(entry);
---

<Default>
  <Container>
    <article>
      <h1>{entry.data.title}</h1>
      
      <Content />
    </article>
  </Container>
</Default>
```

これを記述した後、 `http://localhost:4321/blog/<ファイル名>` (例えば、 `hello.md` なら `http://localhost:4321/blog/hello` ) にアクセスすると、記事が描画されているはずです！

![](/docs/ch2/img/blog_1.png)

### 解説

Astroは `getStaticPaths()` という関数を使うことで、動的にルーティングを設定することができます。こうすることで、Markdownファイルを増やすだけで、自動でURLが設定されるようになり、管理の手間が省けるというわけです。

<details>
<summary>より詳細な解説(TypeScriptに慣れている人向け)</summary>

#### `getStaticPaths()` について

```typescript
export async function getStaticPaths() {
  const blogEntries = await getCollection('blog');
  return blogEntries.map((entry) => ({
    params: { id: entry.id }, // entry.idが/blog/[...id]に対応する
    props: { entry }, // 各ページのPropsにentryを渡す
  }));
}
```

`getStaticPaths()` 内では以下の処理を行っています。

1. Content Collectionから `blog` を読み込む
2. mapメソッドで `params` と `props` の値が入った配列を返す
  - mapメソッドは既にある配列を関数に従って書き換え、新しい配列として出力します。(参考: [MDN Web Docsの解説](https://developer.mozilla.org/ja/docs/Web/JavaScript/Reference/Global_Objects/Array/map))
  - `params: { id: entry.id }` はどのURLのページが生成されるのかを管理しています。今回はURLの `[...id]` という部分に対して `entry.id` (ここにはファイル名が入ります)を対応させるように指定しています。
  - `props: { entry }` はそれぞれのページに渡すデータを設定しています。

#### ページの描画部分

`const { entry } = Astro.props;` で `entry` にそれぞれの記事のデータが入るようになります。このentryの型は以下のようになっています。

```typescript
const entry: {
    id: string;
    body?: string;
    collection: "blog";
    data: InferEntrySchema<"blog">; // schenaで定義した型
    rendered?: RenderedContent;
    filePath?: string;
}
```

つまり例えば記事のタイトルは `entry.data.title` で取り出せる、ということになります。

また、 `const { Content } = await render(entry);` によって、Markdownの本編部分をHTMLに出力してくれます。これを使用しています。

</details>

コミットログ: [65d7757](https://github.com/s-union/astro-hands-on/commit/65d7757d00137748df9a98119d04b977b073ccf6)