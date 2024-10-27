# props
propsとは、コンポーネント間でデータをデータをやり取りするためのReactの基本機能である。
コンポーネントはpropsを引数に受け取り、その値をコンポーネント（UIの部品）に代入し、ReactDOMを返却する。

```jsx
// Squareというコンポーネントにvalueというpropsを受け取っている。
function Square({ value }) {
  // コンポーネントの中では、{props}と記述する。
  return <button className="square">{value}</button>;
}
```
