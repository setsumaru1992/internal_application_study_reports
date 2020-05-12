# ドキュメント

# 気になっている点
- `react-redux`のconnectメソッド（mapStateToPropsとmapDispatchToPropsをReactコンポーネントにつなげるやつ）
- action書くときに`return (dispatch, getRootState) => {})`とか書ける
  - getRootStateが驚きだったから、どんなIFになっているのか。
  - はたまた送ったときにどんな動きをしているのか
    - Promise.resolve()でreturnっぽいことやれることも含めて、値変わったときにめっちゃreducer走査するから、なんでそんなことになってるのか
- Providerって？


## connectメソッド
~~[reduxのcompose](https://github.com/reduxjs/redux/blob/master/src/compose.ts#L56)は単なるHOC(高階コンポーネント)~~
[react-redux](https://github.com/reduxjs/react-redux/blob/master/src/connect/connect.js#L46)はよくわからへんかった。
カリー化で使う2個目の引数は[ここ](https://github.com/reduxjs/react-redux/blob/1f4e45ce920d407835b4b1a1c5d07e13a922ef0e/src/components/connectAdvanced.js#L233)でWrappedCompornentとして使われる
`return hoistStatics(Connect, WrappedComponent)`[出典](https://github.com/reduxjs/react-redux/blob/1f4e45ce920d407835b4b1a1c5d07e13a922ef0e/src/components/connectAdvanced.js#L492)
```js
// https://github.com/mridgway/hoist-non-react-statics/blob/master/src/index.js
export default function hoistNonReactStatics(targetComponent, sourceComponent, blacklist) {
  ...
    return targetComponent;
};
```
まぁ、カリー関数の2つめの引数のReactCompornentを1つめの引数を使ったコンポーネントに移植しているみたい
多分当たり前のように使ってる、stateにselectorを適用したmapStateToPropsとかの値をpropsで使えるようにしてんだろうな

## Action伝播中の引数について
reduxを知るなら[createStore](https://github.com/reduxjs/redux/blob/dc736f1f5155ee85257e6565da474d04bbdda9ee/src/createStore.ts#L50)が元締め。

[dispatch](https://github.com/reduxjs/redux/blob/dc736f1f5155ee85257e6565da474d04bbdda9ee/src/createStore.ts#L225)
```ts
  function dispatch(action: A) {
    if (!isPlainObject(action)) {
      throw new Error(
        'Actions must be plain objects. ' +
          'Use custom middleware for async actions.'
      )
    }

    if (typeof action.type === 'undefined') {
      throw new Error(
        'Actions may not have an undefined "type" property. ' +
          'Have you misspelled a constant?'
      )
    }

    if (isDispatching) {
      throw new Error('Reducers may not dispatch actions.')
    }

    try {
      isDispatching = true
      currentState = currentReducer(currentState, action)
    } finally {
      isDispatching = false
    }

    const listeners = (currentListeners = nextListeners)
    for (let i = 0; i < listeners.length; i++) {
      const listener = listeners[i]
      listener()
    }

    return action
  }
```

ここだけだと`return (dispatch, getRootState) => {})`が何かわからないけど、redux-chunkとかミドルウェア入れたりアクションをreducerに渡す以上の処理もやってるから、そこでミドルウェアのtypeが使えるのか
https://github.com/reduxjs/redux/blob/05bc42c6402693845b9a73175b5be0b368395955/src/types/middleware.ts#L3
```ts
export interface MiddlewareAPI<D extends Dispatch = Dispatch, S = any> {
  dispatch: D
  getState(): S
}
```
ってことは単純でないActionで使える引数はdispatchとstateゲッターか。
https://github.com/reduxjs/redux/blob/8015a5875019c83a5bae67e51ac8c343da89e15a/src/applyMiddleware.ts#L70

# 感想
- [selector](https://blog.isquaredsoftware.com/2017/12/idiomatic-redux-using-reselect-selectors/)
  - selectorはRedux上のmodelでCQRSのQ担当
  - [reselect](https://github.com/reduxjs/reselect)を使うことで複数回stateにアクセスするとしても1回にまとめられるからメモリ的にいい
  - react-reduxの`mapStateToProps`はこれの上位版。一発でreducerにアクセスしてる感じ