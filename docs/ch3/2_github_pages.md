# GitHub Pagesにデプロイしてみよう

さぁ、サイトが完成しました！では、ここからは実際にインターネット上にサイトをアップロードしてみましょう。

> [!NOTE]
> デプロイとは、開発したWebサイトやアプリケーションをインターネット上で公開することです。つまり、世界中の人がアクセスできるようにする作業のことです。

デプロイする先にはレンタルサーバーや[Amazon S3](https://aws.amazon.com/jp/s3/)などのオブジェクトストレージ、[Cloudflare Pages](https://www.cloudflare.com/ja-jp/developer-platform/products/pages/)(イチオシ！)などの専用のホスティングサービスなど色々ありますが、ここではGitHubが提供しているGitHub Pagesを活用していこうと思います。

GitHub Pagesでは、レポジトリからデプロイすると  `https://<あなたのGitHubのユーザー名>.github.io/<GitHubでのレポジトリ名>` が割り当てられます。例えば、このハンズオンでもGitHub Pagesが使われていますが、 https://s-union.github.io/astro-hands-on がトップページです。

## GitHub Pages用の設定をしよう

まず、Astroプロジェクトを管理しているレポジトリを開いて、上のバーの「Settings」から「Pages」を選択します。

そこで、Build and deploymentのSourceを「GitHub Actions」にしてください。

![](/docs/ch3/img/pages_setting.png)

GitHub側の設定はこれで大丈夫です。次に、 `astro.config.ts` を以下のように変更してください。

```diff
import { defineConfig } from 'astro/config';

// https://astro.build/config
export default defineConfig({
+   site: 'https://s-union.github.io', // https://<あなたのGitHubのユーザー名>.github.io
+   base: 'astro-hands-on', // GitHubでのレポジトリ名
});
```

ここの `site` と `base` はGitHubのユーザー名とレポジトリ名で変わります。自分の環境と一致したものに変更してください。

また、これに伴い、リンク参照も一部変更する必要があります。例えば、 `src/components/header.astro` にはリンクがありますが、これを以下のように変更する必要があります(ここも自分の環境と一致したものに変えてください)。

```diff
<ul>
-   <li><a href="/">Home</a></li>
-   <li><a href="/about">About</a></li>
-   <li><a href="/contact">Contact</a></li>
+   <li><a href="/astro-hands-on/">Home</a></li>
+   <li><a href="/astro-hands-on/about">About</a></li>
+   <li><a href="/astro-hands-on/contact">Contact</a></li>
</ul>
```

詳しい変更点はコミットログを参照してください。

コミットログ: [e4527b2](https://github.com/s-union/astro-hands-on/commit/e4527b2208ab7fb93e43e263a29a5f7452044844)

## GitHub Actionsを使おう

今回はデプロイフローにGitHub Actionsを使います。

### GitHub Actionsとは？

GitHub Actionsはソフトウェア開発に用いられる自動化フローツールです。指定した条件を満たすアクションを行う(例: 特定のブランチへのプッシュ)ことでテストコードの実行、コードルールのチェック、ビルドなどを自動で行うことができます。

パブリックレポジトリではこれを無制限で利用することができます。これを利用して「mainブランチにプッシュされたら、GitHub Pagesにデプロイ」を実践していきます。

ちなみに、このようなコードの変更などによって自動的にテストしたりデプロイして実際の環境反映する仕組みのことを **CI/CD** (CI: Continuous Integration (継続的インテグレーション)、CD: Continuous Delivery (継続的デリバリー)) といいます。現代のWebサービスは実運用をしながら開発を行っているため、こういった仕組みが重要となっています。

### GitHub Actionsの使い方

GitHub Actionsを使うには `.github/workflows` 以下に `.yml` ファイルを書くことで利用可能になります。

`.github/workflows/deploy.yml` を以下のように書きます。

```yml
name: Deploy to GitHub Pages

on:
  # Trigger the workflow every time you push to the `main` branch
  # Using a different branch name? Replace `main` with your branch’s name
  push:
    branches: [main]
  # Allows you to run this workflow manually from the Actions tab on GitHub.
  workflow_dispatch:

# Allow this job to clone the repo and create a page deployment
permissions:
  contents: read
  pages: write
  id-token: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout your repository using git
        uses: actions/checkout@v4
      - name: Install, build, and upload your site
        uses: withastro/action@v3
        # with:
        # path: . # The root location of your Astro project inside the repository. (optional)
        # node-version: 20 # The specific version of Node that should be used to build your site. Defaults to 20. (optional)
        # package-manager: pnpm@latest # The Node package manager that should be used to install dependencies and build your site. Automatically detected based on your lockfile. (optional)

  deploy:
    needs: build
    runs-on: ubuntu-latest
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

コミットログ: [e4527b2](https://github.com/s-union/astro-hands-on/commit/e4527b2208ab7fb93e43e263a29a5f7452044844)

このファイルをコミットすると、自動でActionが実行され、ページがデプロイされます。もし失敗したら設定のどれかが間違っているため確認してみてください。

以降、mainブランチに何らかのコミットが行われると自動でデプロイされるようになります。

[次のページへ](/docs/ch3/3_finale.md)