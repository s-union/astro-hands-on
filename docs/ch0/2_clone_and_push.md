# プロジェクトを導入しよう

開発環境が整ったら、実際にプロジェクトを導入して動作させてみましょう！

## 導入方法

```bash
$ pnpm dlx giget gh:s-union/astro-hands-on#giget <プロジェクト名>
```

`<プロジェクト名>` には任意の名前を決めてもらって構いません。実行すると、 `<プロジェクト名>` というフォルダの下にテンプレートが展開されるはずです。

必要なライブラリをインストールしましょう。

```bash
$ cd <プロジェクト名>
$ pnpm install
```

インストールに成功したかを確認するために、開発サーバーを起動してみましょう。

```bash
$ pnpm run dev
```

サーバーが起動し、 http://localhost:4321 に以下のようなページができれば成功です。

![](/docs/ch0/img/astro-init-screenshot.png)

Astroへようこそ 🚀

## GitHubレポジトリを作ろう

さて、近年の開発ではgitを使った開発が主流です[^1]。gitはレポジトリという単位でプロジェクトを管理します。

[^1]: gitやGitHubについては詳細はやりませんが、様々なネット記事で解説していますのでそちらを参照してください。理科大図書館にも良い資料があります。

ここでは、GitHubを利用したレポジトリの管理方法を紹介します。

1. https://github.com にアクセスし、ログインします。
2. **「New」** というボタンをクリックし、レポジトリの作成画面に移ります。

![](/docs/ch0/img/new-repo.png)

- Owner: 自分の名前になっていることを確認
- Repository Name: 導入時に決めた `<プロジェクト名>` と同じ
- Public/Private: **必ずPublicにすること。**　Publicにしないとこの後のハンズオンの一部ができなくなります。
- その他の設定はそのまま

> [!IMPORTANT]
> 本ハンズオンではパブリックレポジトリとして作成するため、世界中の誰でもレポジトリにアクセスできます。これからコード等を書くにあたり、個人情報等を書かないよう留意してください。

3. レポジトリを作成し、Quick SetupのSSHの項目をコピーしておく。

元のプロジェクトに戻り、以下のコマンドを実行する。

```
$ git init -b main
$ git add .
$ git commit -m "initial commit"
$ git remote add origin git@github.com:s-union/astro-training.git # コピーしたものを貼り付ける
$ git push -u origin main
```

成功すると、URLにレポジトリのファイルが生成されているはずです！

![](/docs/ch0/img/github-repo-complete.png)

### コミットをしてみよう

gitは **"commit"** という単位でファイルの更新を保存します。

まだコードの説明をしていませんが、少しファイルを変更してみましょう。

`README.md` を以下のように編集してみます。

```md
# 🚀 Astro ハンズオン 🚀

Astroの学習をはじめました！
```

ファイルを保存して、以下のコマンドを実行します。

```bash
$ git add .
$ git commit -m "READMEの更新"
$ git push
```

<details>

- `git add .`
  - ファイルをステージというコミットの前段階に置きます。 `.` はプロジェクトの全てを表しています。
- `git commit -m "READMEの更新"`
  - コミットします。コミットにはコミットメッセージが必要で、 `-m` プロパティを用いて設定しています。
- `git push`
  - コミットをリモートレポジトリ(この場合はGitHubのこと)にプッシュし、反映させます。

</details>

これでファイルの更新がGitHub側にも反映されました！

### (補足)VSCodeでgit操作

gitのコマンドを覚えるの、大変ですよね。でも大丈夫！VSCodeにはgitを操作するツールがついています！

![](/docs/ch0/img/vscode-git.png)

左側のソース管理を押して、ポチポチするだけで、コミットとプッシュができます！