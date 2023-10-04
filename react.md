## Create React App

```jsx
npx create-react-app [プロジェクト名]
```

↓

```jsx
cd my-app
npm start
```

↓

localhost:3000/にアクセス

## JSX記法

JavaScriptのファイルの中でHTMLのようなタグをタグを書けるというもの

- 第一引数に「`render対象`」、第二引数に「`render箇所`」
- 第一引数
    - 関数名をHTMLのように、タグで囲むことによって、`コンポーネント`として扱える。
- 第二引数
    - rootというidを指定しているが、 public > index.htmlにあるdivタグを指している。

第一引数で関数を呼び出してrenderする内容を指定する、第二引数でrenderして表示する場所を決めるといった感じ。

### JSXのルール

return以降が複数行になる場合は`( )`で囲ってあげる

return以降は1つのタグで囲まれている必要がある

```jsx
import ReactDOM from "react-dom";
// react-domライブラリからReactDOMという名前でモジュールをimport

// Appという名前で、アロー関数で定義した関数を用意
const App = () => {
  return (
    <div>
      <h1>こんにちは！</h1>
      <p>お元気ですか？</p>
    </div>
  );
};

ReactDOM.render(<App />, document.getElementById("root"));
```

ReactDomにはrenderという関数が用意されている

Fragment
書き方は2種類

“react”からFragmentをimportして使用するか、空のタグで囲んでも同じ意味になる

### コンポーネントの使い方

関数で定義されたコンポーネントを関数コンポーネントと呼ぶ

my-app/src/App.jsx

```jsx
export const App = () => {
  return (
    <>
      <h1>こんにちは！</h1>
      <p>お元気ですか？</p>
    </>
  );
};
```

my-app/src/index.js
```
import ReactDOM from "react-dom";
import { App } from "./App.jsx";

ReactDOM.render(<App />, document.getElementById("root"));
```
### イベントやスタイル(CSS)の扱い方

キャメルケース

JSXで書いているHTMLのようなタグの中（return以降など）では、`{ }`で囲むことでJavaScriptを記述できる

```jsx
export const App = () => {
  const onClickButton = () => {
    alert();
  };

  return (
    <>
      {console.log("TEST")}
      <h1>こんにちは！</h1>
      <p>お元気ですか？</p>
      <button onClick={onClickButton}>ボタン</button>
    </>
  );
};
```

### スタイルの扱い方

各タグにstyle属性を記述することでスタイルを適用することができる

⚠️CSSの各要素はJavaScriptのオブジェクトとして記述

```jsx
export const App = () => {
  const onClickButton = () => {
    alert();
  };

  return (
    <>
      <h1 style={{ color: "red" }}>こんにちは！</h1>
      <p>お元気ですか？</p>
      <button onClick={onClickButton}>ボタン</button>
    </>
  );
};
```

`style={ }`のように波カッコで囲み、その中にオブジェクトでCSSに対応する要素を指定していくため`style={{ }}`となる

⚠️redではなく”red”、font-sizeではなくfontSize

ハイフンは認められていない

```jsx
export const App = () => {
  const onClickButton = () => {
    alert();
  };

  const contentStyle = {
    color: "blue",
    fontSize: "20px"
  };

  return (
    <>
      <h1 style={{ color: "red" }}>こんにちは！</h1>
      <p style={contentStyle}>お元気ですか？</p>
      <button onClick={onClickButton}>ボタン</button>
    </>
  );
};
```

⭐️`alert()` の中の `()` は、JavaScriptで関数を呼び出す際に使用する括弧です。この括弧は「関数の実行」を意味します。

`alert` 自体はブラウザの組み込み関数で、小さなダイアログボックスを表示するためのものです。`alert` だけでは関数は実行されませんが、`alert()` のように括弧をつけることで、その関数が実際に実行されます。

`alert()` の中に何も引数を渡さない場合、ダイアログボックスには何もテキストが表示されません。しかし、文字列を引数として渡すことで、その文字列がダイアログボックスに表示されます。

```jsx
alert("こんにちは！");
```

上記のコードを実行すると、ダイアログボックスに「こんにちは！」と表示されます。

まとめると、`alert();` の `()` は、`alert` 関数を実行するためのものであり、この括弧の内部には関数に渡す引数を書くことができます。

⭐️`<h1 style={{ color: "red" }}>こんにちは！</h1>`の波カッコは2つで、 `<p style={contentStyle}>お元気ですか？</p>`の波カッコは1つなのはなぜですか？

良い質問です！この2つの波括弧（`{}`）の使い方にはそれぞれ異なる意味があります。

1. **インラインスタイル**: `<h1 style={{ color: "red" }}>こんにちは！</h1>`
    - こちらの波括弧が2つあるのは、JavaScriptのオブジェクトをReactのJSX内で埋め込むときの文法です。
    - 外側の `{}` は、JSX内でJavaScriptの式を埋め込むためのものです。
    - 内側の `{}` は、JavaScriptのオブジェクトリテラルを表しています。この例では、スタイルのオブジェクトを直接作成しています。
2. **変数の参照**: `<p style={contentStyle}>お元気ですか？</p>`
    - こちらは、既に定義されているJavaScriptの変数（この場合は `contentStyle`）を参照するための波括弧です。この波括弧はJSX内でJavaScriptの式や変数を参照するためのものです。

要するに、

- `<h1 style={{ color: "red" }}>こんにちは！</h1>` はJSX内で直接スタイルオブジェクトを定義しています。
- `<p style={contentStyle}>お元気ですか？</p>` は、既に定義された `contentStyle` という名前の変数をJSX内で参照しています。

この2つの違いを理解することで、ReactのJSXの文法の一部としての波括弧の使い方を理解することができます。

## Props

コンポーネントに渡す引数のようなもので、コンポーネントは受け取ったPropsに応じて表示するスタイルや内容を変化させる

```jsx
export const App = () => {
  const onClickButton = () => {
    alert();
  };

  const contentStyle = {
    color: "blue",
    fontSize: "20px"
  };

  const contentPinkStyle = {
    color: "pink",
    fontSize: "20px"
  };

  return (
    <>
      <h1 style={{ color: "red" }}>こんにちは！</h1>
      <p style={contentStyle}>お元気ですか？</p>
      <p style={contentPinkStyle}>元気です！</p>
      <button onClick={onClickButton}>ボタン</button>
    </>
  );
};
```

上記でもいいが、似たようなstyleを書くのは面倒、コードが長くなる

↓

色とテキストをPropsとして受け取って色付きの文字を返すコンポーネントを作成

ColoredMessageという名前でコンポーネントを作成し、まずは青色で「お元気ですか？」と固定表示するように実装してみる

(componentsというフォルダ内に配置)

my-app/src/App.jsx

```jsx
import { ColoredMessage }  from "./components/ColoredMessage";

export const App = () => {
  const onClickButton = () => {
    alert();
  };

  const contentPinkStyle = {
    color: "pink",
    fontSize: "20px"
  };

  return (
    <>
      <h1 style={{ color: "red" }}>こんにちは！</h1>
      <ColoredMessage />
      <p style={contentPinkStyle}>元気です！</p>
      <button onClick={onClickButton}>ボタン</button>
    </>
  );
};
```

my-app/src/components/ColoredMessage.jsx

```jsx
export const ColoredMessage = () => {
  const contentStyle = {
    color: "blue",
    fontSize: "20px"
  };

  return <p style={contentStyle}>お元気ですか？</p>;
};
```

### Propsの使い方

Propsを使うためには、Propsを渡す方のコンポーネント(App.jsx)と渡される方のコンポーネント(ColoredMessage.jsx)のどちらも修正する必要がある

渡す方はコンポーネントのタグの中に任意の名称をつけてPropsを渡す

colorとmessageをPropsとして渡す

my-app/src/components/ColoredMessage.jsx

```jsx
export const ColoredMessage = (props) => {
  console.log(props);

  const contentStyle = {
    color: props.color,
    fontSize: "20px"
  };

  return <p style={contentStyle}>{props.message}</p>;
};
```

my-app/src/App.jsx

```jsx
import { ColoredMessage }  from "./components/ColoredMessage";

export const App = () => {
  const onClickButton = () => {
    alert();
  };

  return (
    <>
      <h1 style={{ color: "red" }}>こんにちは！</h1>
      <ColoredMessage color="blue" message="お元気ですか？" />
      <ColoredMessage color="pink" message="元気です！" />
      <button onClick={onClickButton}>ボタン</button>
    </>
  );
};
```

### children

テキストをchildrenで渡す

my-app/src/App.jsx

```jsx
import { ColoredMessage }  from "./components/ColoredMessage";

export const App = () => {
  const onClickButton = () => {
    alert();
  };

  return (
    <>
      <h1 style={{ color: "red" }}>こんにちは！</h1>
      <ColoredMessage color="blue">お元気ですか？</ColoredMessage>
      <ColoredMessage color="pink">元気です！</ColoredMessage>
      <button onClick={onClickButton}>ボタン</button>
    </>
  );
};
```

childrenでメッセージを受け取る

my-app/src/components/ColoredMessage.jsx

```jsx
export const ColoredMessage = (props) => {
  console.log(props);

  const contentStyle = {
    color: props.color,
    fontSize: "20px"
  };

  return <p style={contentStyle}>{props.children}</p>;
};
```

### Propsを扱うテクニック

Propsの分割代入

```jsx
export const ColoredMessage = (props) => {
  // Propsを分割代入
  const { color, children } = props;

  const contentStyle = {
    color, // propsが不要、省略記法が使える
    fontSize: "20px"
  };

  // ↓ Propsが不要
  return <p style={contentStyle}>{children}</p>;
};
```

Propsをdestructure(分割代入)するかどうか問題🧐

## State(useState)

コンポーネントの状態を表す値

### useState

関数コンポーネントでは React Hooksと総称される機能群の中の**useState**という関数を用いてStateを扱う

useStateはReactの中に用意されているので、使用する際はimportする必要がある

```jsx
import { useState } from "react";
```

useState関数の返却値は配列の形で1つ目にState変数、2つ目にそのStateを更新するための関数が設定される

```jsx
const [num, setNum] = useState();
```

この場合、**num**が状態を持った変数、**setNum**がそれを更新する関数

useStateは関数なので使用するときは`( )`をつけて関数を実行する

Stateの初期値の設定方法

```jsx
const [num, setNum] = useState(0);
```

数値のStateを定義して画面に表示、ボタン押下時にカウントアップする機能

```jsx
import { useState } from "react";
import { ColoredMessage } from "./components/ColoredMessage";

export const App = () => {
  // Stateの定義
  const [num, setNum] = useState(0);

  // ボタンを押した時にStateをカウントアップ
  const onClickButton = () => {
    setNum(num + 1);
  };

  return (
    <>
      <h1 style={{ color: "red" }}>こんにちは！</h1>
      <ColoredMessage color="blue">お元気ですか？</ColoredMessage>
      <ColoredMessage color="pink">元気です！</ColoredMessage>
      <button onClick={onClickButton}>ボタン</button>
      <p>{num}</p>
    </>
  );
};
```

厳密にはこっちのほうがいいらしい

```jsx
import { useState } from "react";
import { ColoredMessage } from "./components/ColoredMessage";

export const App = () => {
  // Stateの定義
  const [num, setNum] = useState(0);

  // ボタンを押した時にStateをカウントアップ
  const onClickButton = () => {
    // setNum(num + 1);
    setNum((prev) => prev + 1);
  };

  return (
    <>
      <h1 style={{ color: "red" }}>こんにちは！</h1>
      <ColoredMessage color="blue">お元気ですか？</ColoredMessage>
      <ColoredMessage color="pink">元気です！</ColoredMessage>
      <button onClick={onClickButton}>ボタン</button>
      <p>{num}</p>
    </>
  );
};
```

## 再レンダリングと副作用

State更新時にコンポーネントが再レンダリングされ、関数コンポーネントが再度頭から実行される

変更を検知してコンポーネントを再処理すること→再レンダリング

### 副作用とuseEffect

コンポーネントの副作用を制御する機能

useStateと同様にReactからimportする

```jsx
import { useEffect } from = "react";
```

useEffectの宣言

```jsx
useEffect(実行する関数, [依存する値]);
```

ある値が変わった時に限り、ある処理を実行する機能

例：Stateの値が変わった時のみアラートを表示する

```jsx
export const App = () => {

  useEffect(() => {
    alert))();
}, [num]);
  return (
    {/* 省略 */}
  );
};
```

第一引数にはアロー関数で処理を記述、第二引数は必ず配列で指定

複数指定する場合は`[num, num2]`のように書く

⚠️useEffectは依存配列にしている値が変わった時に加え、コンポーネントのマウント時(一番最初)にも必ず実行される

→useEffectの第二引数に[ ]を指定すると「コンポーネントを表示した初回のみ実行するような処理」を記述できる

画面を表示して初期データを取得するときなどによく使用される

コンポーネントは再レンダリングを何度も繰り返している
