# JavaScript/TypeScriptに慣れよう

この項目ではJavaScriptの基本を学びます。JavaScriptには大量の構文があるので、全てを網羅することはできませんが、Astroの学習に必要なほんの少しを学んでいきましょう。

## はじめのJavaScript

今回はNode.jsでJavaScriptを実行します。

プロジェクトの直下に `index.js` を書きましょう。

```js
console.log('Hello World!')
```

早速実行してみましょう。以下のコマンドを実行します。

```bash
$ node index.js
```

コンソールに `Hello World!` と表示されましたか？

## 変数と型

続けて、 `index.js` を編集します。

```js
const number = 123; // number型
const string = 'Hello'; // string型
let boolean = true; // boolean型

console.log(typeof number); // 型の形式を出力
console.log(number);
console.log(typeof string);
console.log(string);
console.log(typeof boolean);
console.log(boolean);

boolean = false; // letは更新可能

console.log(boolean);

const array = ['apple', 'banana', 'orange']; // array型

console.log(typeof array);
console.log(array);
console.log(array[0]);

const object = {
  name: 'John',
  age: 30,
  isStudent: false,
}; // object型

console.log(typeof object);
console.log(object);
console.log(object.name);
```

これを実行してみると色々出力されますよね。順番に見ていきましょう。

### 変数の定義

変数とはデータを格納しておく箱のようなものです。

JavaScriptには2つの変数があります。

- `const variable = ...`
  - constは変更不可能です。
- `let varivable = ...`
  - letは変更可能です。
  - `variable = ...` という形で代入する値を変えられます。

> [!NOTE]
> 古いJavaScriptの記事だと `var variable = ...` のように `var` で定義しているものがありますが現在は非推奨です。

### 型

あらゆるデータには **型** というどのようなデータを扱うかの指定がついています。JavaScriptは動的に型を判断しています。

#### 型の一覧

| 型名      | 説明                               | 具体例                |
| --------- | ---------------------------------- | --------------------- |
| number    | 数値を表します。                   | `123`                 |
| string    | 文字列を表します。                 | `'something'`         |
| boolean   | 真偽のどちらかを表します           | `true` または `false` |
| null      | 値がないことを表します。           | `null`                |
| undefined | 値が未定義のことを表します。       | `undefined`           |
| array     | 値の配列を表します。               | `[1, 2, 3]`           |
| object    | 名前つきのオブジェクトを表します。 | `{name: 'John'}`      |

## 関数

`index.js` を以下のように編集します。

```js
function addNumber(a, b) {
  return a + b;
}

const subtractNumber = (a, b) => {
  return a - b;
};

const multiplyNumber = function (a, b) {
  return a * b;
}; // 通常の関数

console.log(addNumber(5, 3)); // Output: 8
console.log(subtractNumber(5, 3)); // Output: 2
console.log(multiplyNumber(5, 3)); // Output: 15

```

実行すると、8と2が出力されるはずです。

JavaScriptには関数定義の方法が2つあります。通常の関数宣言とアロー関数です。

アロー関数は比較的近年できた方法です。短く書けるので推奨している人も多いです。

特にmapメソッドなどは圧倒的に楽になります。

```js
const numArray = [1, 2, 3]
const doubled = numArray.map((num) => num * 2) // アロー関数は一行ならこれだけでOK

console.log(doubled) // [2, 4, 6]
```

## import/export構文

JavaScriptでは、特定の関数や値をエクスポートして、別のファイルから読み込ませる、ということもできます。

まず、 `lib.js` というファイルを作り、以下のように記述します。

```js
export const addNumber = (a, b) => {
  return a + b;
};

const magicNumber = 42;

export default magicNumber;
```

次に、 `index.js` に以下のように書きましょう。

```js
import { addNumber } from './lib.js';
import magicNumber from './lib'

console.log(addNumber(1, 2)); // 3
console.log(magicNumber); // 42
```

`export` した関数や変数を `import` を介して取得できていますね。

### named exportとdefault export

サンプルコードでは2つのexportの方式がありました。

```js
export const addNumber = (a, b) => {
  return a + b;
};
```

のようにそのままexportしているものと、

```js
const addNumber = (a, b) => {
  return a + b;
};
export default addNumber
```

のように `default` というワードが入っているものです。

これはそれぞれ **named export** 、 **default export** と呼ばれ、微妙に制約が異なります。

#### named export

named export(名前付きエクスポート)は1つのファイル内でいくつも使うことができます。ただし、名前をインポート側で変更できません。

```js
// lib.js エクスポート側
export const addNumber = (a, b) => {
  return a + b;
};

export const subtractNumber = (a, b) => {
  return a - b;
};
```

```js
// index.js インポート側
import { addNumber, substractNumber } from './lib' // 名前は固定される

console.log(addNumber(5, 3)); // Output: 8
console.log(subtractNumber(5, 3)); // Output: 2
```

#### default import

`export default` という構文を用います。1ファイルあたり1つしか使うことができませんが、インポート側で名前を変更することができます。

```js
// lib.js エクスポート側
const addNumber = (a, b) => {
  return a + b;
};

export default addNumber
```

```js
// index.js インポート側
import yourOwnNamedFunction from './lib' // 名前は固定されず、好きな名前で使える

console.log(yourOwnNamedFunction(5, 3)); // Output: 8
```

## TypeScriptへ

さて、ここまででJavaScriptの基礎構文を勉強してもらいましたが、ここからはTypeScriptについても見ていきましょう。

改めて、 `index.js` に以下のコードを書いてください。

```js
const addNumber = (a, b) => {
  return a + b;
};

console.log(addNumber(1, 2)); // 3
```

このコードは `addNumber` に2つの数字を渡すことで、その足し算をする関数ですが、実はこれ、**文字列を入れることができてしまいます。**

```diff
const addNumber = (a, b) => {
  return a + b;
};

- console.log(addNumber(1, 2)); // 3
+ console.log(addNumber(1, '2')); // 12
```

これはJavaScriptの仕様で、文字列型が優先されるのです。これは意図していない動作ですよね。

では、これを防ぐにはどうしたらいいでしょうか。ここで登場するのが **TypeScript** です。

### TypeScriptの初歩

TypeScriptは、2012年にMicrosoftが公開した、JavaScript本来の仕様に型付けなどの機能を追加した言語です。

まずは実際に使ってみましょう。 `index.js` を `index.ts` にリネームし、以下のように書き換えてください。

```ts
const addNumber = (a: number, b: number) => {
  return a + b;
};

console.log(addNumber(1, 2)); // 3
```

先ほどのコードから型の定義部分が増えていますね。

Node.jsはTypeScriptを直接実行できないので、まず `.ts` ファイルを `.js` ファイルに変換する必要があります[^1]。 `tsc` というコマンドが型の検査と `.js` への変換をやってくれます。

[^1]: 2025年5月現在、Node.js環境における[tsファイルの実行は実装されています](https://nodejs.org/en/blog/release/v23.6.0)が、安定版(LTS)ではExperimentalです。tsファイルの実行には[ts-node](https://www.npmjs.com/package/ts-node)や[tsx](https://tsx.is/)のような実行ライブラリ、または[Bun](https://bun.sh/)や[Deno](https://deno.com/)のようなts対応のランタイムを利用するといいでしょう。

```bash
$ pnpm tsc index.ts
```

変換された `index.js` を見てみましょう。

```js
const addNumber = (a, b) => {
    return a + b;
};
console.log(addNumber(1, 2)); // 3
```

型定義部分が無くなっているのが分かりますね。これで実行できます。

では、先ほどのように文字列を挿入したらどうなるでしょうか。

```ts
const addNumber = (a: number, b: number) => {
  return a + b;
};

console.log(addNumber(1, '2')); // 型エラーになる
```

実行結果

```
index.ts:5:26 - error TS2345: Argument of type 'string' is not assignable to parameter of type 'number'.

5 console.log(addNumber(1, '2')); // error
                           ~~~


Found 1 error in index.ts:5
```

きちんとエラーが出てくれました。これでバグを未然に防ぐことができましたね。

このように、プログラムが実行される際に、データ型に矛盾が生じないことを保証することを **型安全性** と呼びます。

TypeScriptは **JavaScriptの型安全を高めた言語** といえるでしょう。

### 型定義の `type` と `interface`

より複雑な型を表現するために、TypeScriptでは `type` と `interface` が用意されています。

```ts
type Post = {
  id: number;
  title: string;
  tag: string[];
  content: string;
  createdAt: Date;
  updatedAt: Date;
};

interface PostList {
  posts: Post[];
  total: number;
  page: number;
}
```

コードのように、型定義内で他の型定義を利用することもできます。

## TypeScriptのメリット

型安全性のメリットはただエラーを事前に検知できるだけではありません。

- 型定義によってコードの可読性が向上する
- VSCodeなどのIDEの補完が効く
- AIコーディングツールの支えになる

特にIDEによる補完の存在は大きいです。これだけでコーディングスピードが桁違いに上がります。

![](/docs/ch0/img/ts-ide-server.png)

## おしまい！

これでこのチャプターは終了です！お疲れ様でした！

JavaScriptの変数・型・関数、そしてTypeScriptの型チェックはこれからのAstroでのプログラミングでも出てきますのできちんと覚えておきましょう！

[次のページへ](/docs/ch1/1_start_astro.md)