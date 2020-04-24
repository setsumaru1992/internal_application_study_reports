# jsでfalseとみなされる値
[参考](https://qiita.com/Imamotty/items/bc659569239379dded55#%E3%81%8A%E3%81%BE%E3%81%91%EF%BC%91false%E3%81%A8%E8%A6%8B%E3%82%8B%E3%81%93%E3%81%A8%E3%81%8C%E3%81%A7%E3%81%8D%E3%82%8B%E5%80%A4)
- 0
- -0
- null
- false
- NaN
- undefined
- 空文字列 ("")
  
上記以外はtrueとみなされる

[そのため以下に注意](https://qiita.com/__mick/items/ea30e3efb1cbff3ae35e)
- 空配列はtrue
- 空オブジェクトもtrue

# ||記法・&&記法
[ドキュメント](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Logical_Operators)
上記を参考に実際に使われる記法を備忘録として記載
## ||記法
`let player = name || 'anonymous';`
はRubyでいう
`player = name.presence || 'anonymous';`

## &&記法
&&記法は純粋に論理値チックな判断
前者がfalseに値する値だったら、その値を返し、trueに値するなら後者を返す
```js
true && 5 // 5
false && 5 // false
null && 5 // null
1 && 5 // 5
0 && 5 // 0
```

