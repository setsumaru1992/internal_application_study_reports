# ドキュメント
https://reactjs.org/docs/getting-started.html

# 主に知りたいこと
- Reactのrefとかと一緒に出てくるcontextって何？そういうReactの基本構成を知りたい。ForwardRefとかmemoとかも


## [ref](https://reactjs.org/docs/refs-and-the-dom.html)
  コンストラクタでrefを作り、DOM要素の中でrefを埋め込む
  
  onclickイベントとかで`this.textInput.current.focus();`とかみたいにrefで追える要素を操作する
  
  クラスコンポーネント全体にもref張れる`<CustomTextInput ref={this.textInput} />`
  Butクラスコンポーネント全体じゃなくクラスコンポーネント内の1要素にrefを当てたいなら、ForwardingRefでref指定を伝播させる([ドキュメント](https://reactjs.org/docs/forwarding-refs.html))

  HOC(高階コンポーネント)を使う場合、refとforwardedRefを1ファイルに完結させて、上のコンポーネントで子コンポーネントを操作できる。([ドキュメント](https://reactjs.org/docs/forwarding-refs.html#forwarding-refs-in-higher-order-components))

## [context](https://reactjs.org/docs/context.html)
> Context provides a way to share values like these between components without having to explicitly pass a prop through every level of the tree.(e.g. locale preference, UI theme) 

配下で共通の値をpropsに使わなきゃいけないのが違うということで。

contextの値はProviderタグ内でグローバルに使用可能。以下の場合はダークモードを適用（デフォルトはライトモード）
```js
const ThemeContext = React.createContext('light');

class App extends React.Component {
  render() {
    // Use a Provider to pass the current theme to the tree below.
    // Any component can read it, no matter how deep it is.
    // In this example, we're passing "dark" as the current value.
    return (
      <ThemeContext.Provider value="dark">
        <Toolbar />
      </ThemeContext.Provider>
    );
  }
}
```

~Context.Consumerでcontextの値を変えられる

Providerはネストさせることで複数適用可能

## [Functions as Children](https://reactjs.org/docs/jsx-in-depth.html#functions-as-children)
```js
// Calls the children callback numTimes to produce a repeated component
function Repeat(props) {
  let items = [];
  for (let i = 0; i < props.numTimes; i++) {
    items.push(props.children(i));
  }
  return <div>{items}</div>;
}

function ListOfTenThings() {
  return (
    <Repeat numTimes={10}>
      {(index) => <div key={index}>This is item {index} in the list</div>}
    </Repeat>
  );
}
```
`props.children(i)`と書くと、子要素ではrubyのyield的な書き方ができる

## [portals](https://reactjs.org/docs/portals.html)
なんかportal便利そう。今いる位置と完全別個にいろいろできる
モーダルや固定ヘッダとか。
技術検証したい

[神出鬼没な場所にマウントする例](https://codesandbox.io/s/m3zkymwq5x?file=/index.js)
[親コンポーネントのstateによってportalを出し分け](https://codesandbox.io/s/6yx5o1qpz)
[メリット](https://qiita.com/jkr_2255/items/96d3396420765c595f04)

以下みたいな感じで固定ヘッダとか実装できそう
```js
if(sticky){
  // 固定化エリアに出す
} else {
  // 既存の子要素の所に出す
}
```

## [renderProps](https://reactjs.org/docs/render-props.html)
renderPropsを指定すると、親要素で指定した要素を、子要素側で指定した所に注入できる。
親がchildrenを自由に配置することの逆版かな

# 感想
- [Add React to a Website](https://reactjs.org/docs/add-react-to-a-website.html)を見てwebpackでビルドするnode環境じゃないとreact使えないと思ってたけど、そうじゃなくて驚いた。importとかできないからめっちゃグローバル環境で書くことになると思うんだけど