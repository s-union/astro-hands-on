# 環境の確認をしよう

## 前提条件

以下の導入、もしくはアカウントの作成が済んでいることが必要です。

- [Visual Studio Code](https://code.visualstudio.com)
  - プログラミングをするエディタです。
- [Node.js](https://nodejs.org/ja)
  - プログラム(JavaScript)を動作させるランタイムです。
- [pnpm](https://pnpm.io/ja/)
  - パッケージマネージャーと呼ばれる、Node.jsのパッケージや実行などの機能を管理するツールです。
  - デフォルトで付属するnpmでも十分ですが、パフォーマンスなどにメリットがあります。
- [git](https://git-scm.com)
  - コミットという単位でファイルの更新履歴を管理するバージョン管理システムです。
- [GitHub](https://github.com)
  - gitのレポジトリをインターネット上に上げるサービスです。
  - 学生は有料版が無料で使えます。GitHub CopilotというAIがコード書いてくれるサービスも無料です。

### コマンドの確認

導入ができていることの確認として、ターミナルでコマンドを実行してみましょう。

Windowsならば「Windows Terminal」もしくは「コマンドプロンプト」、Macならば「ターミナル」というソフトを起動し、以下のように実行してみましょう。

```bash
$ node -v
```

>[!NOTE]
> ここでの `$` はコマンド実行の先頭であることを表しています。この場合、あなたが入力するのは `node -v` だけです。

導入に成功しているならば、バージョンが表示されるはずです。

![cmd](/docs/ch0/img/cmd.jpg)

同様に、その他のコマンドも確認しておきましょう。

```bash
$ git -v
$ pnpm -v
```

### SSHとGitの設定

SSHはリモートのコンピュータに対しファイル送信やコマンドの実行などを暗号化した通信で行ってくれるプロトコルです。

gitとGitHub間の通信を安全なものにするために導入する必要があります。

- Windowsの場合: [こちら](https://zenn.dev/aoikoala/articles/388eb861249780)
- Macの場合: [こちら](https://qiita.com/ucan-lab/items/e02f2d3a35f266631f24)

完了したら、gitの設定を変更します。

```bash
$ git config --global user.name "<YOUR_NAME_HERE>"
$ git config --global user.email "<YOUR_EMAIL_HERE>"
```

`YOUR_NAME_HERE` と `YOUR_EMAIL_HERE` の部分は自分の名前とメールアドレスを入力しましょう。

全ての設定が完了したら、GitHubに繋がるか確認しましょう！

```bash
$ ssh -T git@github.com
```

`Hi <GITHUB_NAME>! You've successfully authenticated, but GitHub does not provide shell access.` と返ってきたら成功です！

[次のページへ](/docs/ch0/2_clone_and_push.md)