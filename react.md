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

- 第一引数に「**render対象**」、第二引数に「**render箇所**」
- 第一引数
    - 関数名をHTMLのように、タグで囲むことによって、**コンポーネント**として扱える。
- 第二引数
    - rootというidを指定しているが、 public > index.htmlにあるdivタグを指している。

第一引数で関数を呼び出してrenderする内容を指定する、第二引数でrenderして表示する場所を決めるといった感じ。

### JSXのルール

return以降が複数行になる場合は**( )**で囲ってあげる

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

**Fragment**

書き方は2種類

“react”からFragmentをimportして使用するか、空のタグで囲んでも同じ意味になる




