# Astroを触ってみよう

チャプター1へようこそ！ここからは実際にAstroを使ってブログサイトを作っていきましょう。

## サンプルコード、コミットログの見方について

サンプルコードは[こちらに](https://github.com/s-union/astro-hands-on)全て記載されています。

また、コードの変更点はコミットログで確認できるようにしています。合わせて活用してください。

![](/docs/ch1/img/commitlog.png)

## 開発サーバーを立ち上げよう

まずは開発サーバーを立ち上げてみましょう。ターミナルに以下のコマンドを実行します。

```bash
$ pnpm run dev
```

チャプター0で確認に使ったコマンドと同じですね！こんな画面のページを開けましたか？

![](/docs/ch0/img/astro-init-screenshot.png)

### ファイルを編集してみる

今見ているページは `src/pages/index.astro` というファイルを参照しています。

試しに変更してみましょう。 **開発サーバーを停止せずに** `<h1>` タグをこのように書き換えます。

```diff
---

---

<html lang="ja">
	<head>
		<meta charset="utf-8" />
		<meta name="viewport" content="width=device-width" />
		<meta name="generator" content={Astro.generator} />
		<title>Astro</title>
	</head>
	<body>
-    <h1>Astro</h1>
+    <h1>Hello World!</h1>
	</body>
</html>
```

コミットログ: [b6eca59](https://github.com/s-union/astro-hands-on/commit/b6eca590fbfff23b90444b5806eb6d6af4d564b0)

保存すると開発サーバーが自動で更新されていることが分かるはずです！このように、コードと開発サーバーを行き来しながらコードを書いていくことになります。

[次のページへ](/docs/ch1/2_astro_concept.md)