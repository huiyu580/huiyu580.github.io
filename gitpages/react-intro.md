# React 基本介紹

## 特性

- 單向資料流，只能從父母元件到子女元件，vue & angular 為雙向
  1. 依靠 props 來傳遞資料
  2. 優點：在複雜結構中容易除錯與最佳化
- react 建立虛擬 DOM，先做差異比較(reconcilation)再渲染(render)
- 以元件為基礎的開發方式
  1. 以類別或函式，加入狀態(state)與屬性(props)特性來開發元件
  2. 拆分可重複利用的功能和介面為 component 後，再組合他們
- 宣告式程式開發
  1. 建立容易維護與除錯的應用程式

## JSX 語法

- 在 JSX 中使用{}嵌入 JS 表達式，具有求值運算的功能，不能使用 if else 判斷式，但可以使用三元運算子，logical OR 和 logical AND

```javascript=
condition ? exprIfTrue : exprIfFalse
```

- 一個 render 方法中(即函式型元件的 return)，只能有一個根元素回傳

```javascript=
return (
    <>
        <h1>Title</h1>
        <p>content</p>
    </>
)
```
- React.Fragment元件`<></>`不會產生多餘的render標記
- 因為react使用XHTML，因此自我封閉的元素結尾必須封閉
```javascript=
<img src="" />
<input type="" />
<hr />
<br />
```
- 自訂元件英文大寫開頭，HTML元素小寫開頭
- 元件加入事件為on開頭，屬性值為函式
```javascript=
<h2 onClick={() => setCount(count + 1)}>{count}</h2>
```
- JS關鍵字的屬性名稱會更改 ex. class -> className ; for -> htmlFor
- style屬性為物件值
```javascript=
<p style={{color:'red'}}>content</p>
```
- 列表標記項目，要給key屬性，避免列表中的重複內容
```javascript=
const todoItems = todos.map(
    (todo) => <li key={todo.id}>{todo.text}</li>
)
```