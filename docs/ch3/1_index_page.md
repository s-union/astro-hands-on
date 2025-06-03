# トップページを完成させよう

チャプター3へようこそ！このチャプターではAstro学習の締めくくりとして、トップページの作成と、オンライン上へのデプロイをやってみましょう。

## ブログカードを作ろう

まずはそれぞれの記事についてのカードコンポーネントを作ります。

`src/components/blogcard.astro` に以下のコードを記述します。

```astro
---
// src/components/blogcard.astro
import { Image } from "astro:assets";
import type { CollectionEntry } from "astro:content";

interface ImageModule {
	default: ImageMetadata;
}

interface Props {
	entry: CollectionEntry<'blog'>;
	image?: ImageModule;
}

const { entry, image } = Astro.props;
---

<div class="blog-card">
	<a href={`/astro-hands-on/blog/${entry.id}`} class="blog-card__link">
		<div class="blog-card__image">
			{image && (
				<Image
					src={image.default}
					alt={entry.data.title}
					width={400}
					height={200}
					loading="lazy"
				/>
			)}
		</div>
		<div class="blog-card__content">
			<h3 class="blog-card__title">{entry.data.title}</h3>
			<div class="blog-card__meta">
				<time class="blog-card__date">{entry.data.created}</time>
				{entry.data.updated && entry.data.updated !== entry.data.created && (
					<span class="blog-card__updated">更新: {entry.data.updated}</span>
				)}
			</div>
		</div>
	</a>
</div>

<style>
.blog-card {
	background: white;
	border-radius: 12px;
	box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
	overflow: hidden;
	transition: transform 0.3s ease, box-shadow 0.3s ease;

	&:hover {
		transform: translateY(-5px);
		box-shadow: 0 8px 25px rgba(0, 0, 0, 0.15);

		.blog-card__image img {
			transform: scale(1.05);
		}
	}
}

.blog-card__link {
	display: block;
	text-decoration: none;
	color: inherit;
	height: 100%;
}

.blog-card__image {
	width: 100%;
	height: 180px;
	overflow: hidden;
	position: relative;

	img {
		width: 100%;
		height: 100%;
		object-fit: cover;
		transition: transform 0.3s ease;
	}
}

.blog-card__content {
	padding: 1.25rem;
}

.blog-card__title {
	margin: 0 0 0.75rem 0;
	font-size: 1.125rem;
	font-weight: 600;
	line-height: 1.4;
	color: #333;
}

.blog-card__meta {
	display: flex;
	flex-direction: column;
	gap: 0.25rem;
	font-size: 0.875rem;
	color: #666;
}

.blog-card__date {
	font-weight: 500;
}

.blog-card__updated {
	font-style: italic;
	color: #888;
}
</style>
```

`entry` と `image` をPropsに指定することで、再利用しやすくしています。

## トップページを書き換えよう

さぁ最後です！トップページにカバー画像と投稿一覧を作成しましょう。

`src/pages/index.astro` に記述します。

```astro
---
// src/pages/index.astro
import { Image } from "astro:assets";
import { getCollection } from 'astro:content';
import BlogCard from "../components/blogcard.astro";
import Container from "../components/container.astro";
import Title from "../components/title.astro";
import Default from "../layouts/default.astro";

import cover from '../images/cover.jpg';

// ブログ記事をすべて取得
const blogEntries = await getCollection('blog');

// 画像のインポート（画像ファイルを一括で読み込む）
interface ImageModule {
  default: ImageMetadata;
}
const imageModules = import.meta.glob<ImageModule>('../images/*.{png,jpg,jpeg,gif,webp,avif}', { eager: true });
---

<Default>
	<main>
		<div class="cover">
			<Image
				src={cover}
				alt="Cover"
				class="cover__image"
				width={1280}
				loading="eager"
			/>
		</div>
		<Container>
			<Title title="Welcome to My Astro Site" />
			<p class="intro-text">
				このサイトはAstroを使用して構築されたサンプルサイトです。最新のブログ記事やプロジェクト情報をチェックしてください。
			</p>
			
			<!-- ブログ記事一覧セクション -->
			<section class="blog-section">
				<h2 class="blog-section__title">最新のブログ記事</h2>
				<div class="blog-grid">
					{blogEntries.map((entry) => {
						const image = imageModules[`../images/${entry.data.cover}`];
						return (
							<BlogCard entry={entry} image={image} />
						);
					})}
				</div>
			</section>
		</Container>
	</main>
</Default>

<style>
.cover {
	width: 100%;
	height: 300px;
	overflow: hidden;
	img {
		width: 100%;
		height: auto;
	}
}

.blog-section {
	margin-top: 3rem;
}

.blog-section__title {
	font-size: 1.75rem;
	font-weight: 700;
	margin-bottom: 2rem;
	text-align: center;
	color: #333;
	position: relative;
}

.blog-grid {
	display: grid;
	grid-template-columns: repeat(auto-fit, minmax(240px, 1fr));
	gap: 1.5rem;
	margin-bottom: 2.5rem;

	@media (min-width: 768px) {
		grid-template-columns: repeat(auto-fit, minmax(320px, 1fr));
		gap: 2rem;
	}
}
</style>
```

> [!NOTE]
> `eager: true`は画像ファイルを「すぐに読み込む」設定です。通常は必要な時だけ読み込みますが、この設定により、最初からすべての画像を読み込むようになります。

コミットログ: [7c962eb](https://github.com/s-union/astro-hands-on/commit/7c962eb548e88eec61a37c0b951d050943dbe9b2)

### 解説

今回はmapメソッドを利用して要素を並べています。

<details>
<summary>より詳細な解説</summary>

JSX記法では、mapメソッドの戻り値に要素を返すと配列に従って要素を並べます。

例えば、

```tsx
const names = ['Tom', 'John', 'Mary']

<div>
  {names.map((name) => {
    <div>{ name }</div>
  })}
</div>
```

のとき、

```tsx
<div>
  <div>Tom</div>
  <div>John</div>
  <div>Mary</div>
</div>
```

のように変換されるわけです。

</details>

## 完成！！

![](/docs/ch3/img/index_page.png)

長らくのコーディングお疲れ様でした！これでAstro部分は全て完成です！！

[次のページへ](/docs/ch3/2_github_pages.md)