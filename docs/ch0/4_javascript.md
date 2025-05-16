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

JavaScriptには2つの変数があります。

- `const variable = ...`
  - constは変更不可能です。
- `let varivable = ...`
  - letは変更可能です。
  - `variable = ...` という形で代入する値を変えられます。

### 型

あらゆる変数や