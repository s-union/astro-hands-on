# ブログのスタイルを調整しよう

ここまででブログの記事を表示させることができましたが少し味気無いですね。CSSを書いてスタイルを調整していきましょう。

## 画像ファイルを読み込む

まずはサムネイルを読み込みましょう。

`src/pages/blog/[...id].astro` に以下のように追記していきます。

```astro
---
import { Image } from 'astro:assets';
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

interface ImageModule {
  default: ImageMetadata;
}
const imageModules = import.meta.glob<ImageModule>('../../images/*.{png,jpg,jpeg,gif,webp,avif}', { eager: true });
const image = imageModules[`../../images/${entry.data.cover}`];
---

<Default>
  <Container>
    <article class="content">
      <h1 class="content__title">{entry.data.title}</h1>
      <div class="content__cover">
        <Image
          src={image.default}
          alt={entry.data.title}
        />
      </div>
      <div class="content__body">
        <Content />
      </div>
    </article>
  </Container>
</Default>

<style>
.content {
  width: 100%;
  margin-inline: auto;

  @media screen and (min-width: 768px) {
    width: 80%;
  }
}

.content__cover {
  width: 100%;
  height: auto;
  text-align: center;
  margin-bottom: 2rem;

  img {
    width: 100%;
    height: auto;
    margin-inline: auto;
  }
}

</style>
```

Astroには `<Image />` というコンポーネントがあります。このコンポーネントに画像を渡すと、画像を自動で圧縮し、 `.webp` という拡張子で出力してくれます。ただファイルサイズが小さくなるだけでなく、現代のWebサイトは圧縮した画像形式である `.webp` か `.avif` であることが求められているので、これはとてもありがたい機能ですよね。

## 残りのスタイルも調整する

ラストスパートです！残りの部分も書いてしまいましょう。

```diff
---
import { Image } from 'astro:assets';
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

interface ImageModule {
  default: ImageMetadata;
}
const imageModules = import.meta.glob<ImageModule>('../../images/*.{png,jpg,jpeg,gif,webp,avif}', { eager: true });
const image = imageModules[`../../images/${entry.data.cover}`];
---

<Default>
  <Container>
    <article class="content">
      <h1 class="content__title">{entry.data.title}</h1>
+       <div class="content__meta">
+         <div class="content__created">
+           制作日時: {entry.data.created}
+         </div>
+         <div class="content__updated">
+           更新日時: {entry.data.updated ?? entry.data.created}
+         </div>
+       </div>
      <div class="content__cover">
        <Image
          src={image.default}
          alt={entry.data.title}
        />
      </div>
      <div class="content__body">
        <Content />
      </div>
    </article>
  </Container>
</Default>

<style>
.content {
  width: 100%;
  margin-inline: auto;

  @media screen and (min-width: 768px) {
    width: 80%;
  }
}

+ .content__title {
+   margin-bottom: 0;
+   border-bottom: 1px solid #ccc;
+   padding-inline: 1rem;
+ }
+ 
+ .content__meta {
+   padding: 0.5rem;
+   display: flex;
+   gap: 1rem;
+   margin-bottom: 1rem;
+   color: #666;
+ }
+ 
.content__cover {
  width: 100%;
  height: auto;
  text-align: center;
  margin-bottom: 2rem;

  img {
    width: 100%;
    height: auto;
    margin-inline: auto;
  }
}

</style>
```

コミットログ: [d3ce4d3](https://github.com/s-union/astro-hands-on/commit/d3ce4d3bb37c484b7db81cff1f0800c2ed877b48)

ここまで来ればブログ記事部分の実装は完了です！お連れ様でした。

次回はトップページを完成させ、実際にページをデプロイしていきましょう！

[次のページへ](/docs/ch3/1_index_page.md)