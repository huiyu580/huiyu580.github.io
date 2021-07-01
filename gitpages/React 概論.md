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

## 類別型元件 vs 函式型元件
生命週期: 類別型元件有，函式型原件為模擬(useEffect hook)
狀態   :  類別型元件可以使用，函式型元件使用(useState hook)

?? 會混用嗎??

## 狀態
- 因為使用者操作後，而不斷改變的資料值
- 與使用者互動性有關
- 設計元件時應該以狀態為最優先的思考重點  
- 類別型元件將狀態放在constructor
- 函式型元件將狀態以解構賦值的方式
- useState(0)會回傳一個陣列，0為初始值  

```javscript=
const [total, setTotal] = useState(0)
```  

- 不可以直接更動state，只能使用setState()
- 類別型元件在setTotal參數傳入物件
- 函式型元件沒辦法使用updater ??



- setState異步執行，但不是js的非同步，也不是promise物件
  - 解決辦法:
    1. 先用變數接住最後更動後的值 
    2. 使用生命週期方法
    3. 使用setState的第二個傳入參數(cb)



### 屬性
- 傳遞資料的方法
- props為唯獨，不能去改變值
- 元件本身無法控制自己是否被render，只有父母元件可以

## 其他
JSX語法中不能放物件，但可以放物件
箭頭函式盡量使用花括號＋return 避免之後變成多行時，要做更動

### logical AND
盡量使用布林值
```javascript=
<>
  function App(){
    const [total, setTotal] = useState(0)
    return (
      <h3>第一種</h3>
      {total && <p>total has value</p>}
      <h3>第二種</h3>
      {total !== 0 && <p>total has value</p>}
      <h3>第三種</h3>
      {!!total && <p>total has value</p>}
    )
  }

```

### 純函式 pure function
- 不依賴外部的變數(環境變數值)
- 

### 解構賦值
- 總是使用const宣告

