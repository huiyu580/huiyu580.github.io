# useRef()
- const reference = useRef(initialValue)
- react 提供為真實DOM元件實體參照的物件，使用時要加上.current，才能找到真實DOM實體的參照物件

## 使用時機
- 整合第三方應用時，ex. Map, 圖表, 動畫, DOM處理
- 表單元素撰寫聚焦or撰寫文字功能時
- 音樂影片撥放功能
- web animation api

# 生命週期方法 lifecycle

- 設計給類別型元件使用

## componentDidMount 的使用時機

- 載入頁面時從伺服器要資料時
- 使用例如 map 等 api 時

## componentDidUpdate 的使用時機

- 解決 setState 的異步問題

- 觸發 componentDidUpdate 的時機:
    - 元件本身狀態改變，或是從父母元件拿到新的屬性
    - state 是私有的，所以父母不知道子女狀態的改變

# useEffect
- 在函式型元件中，可以使用useEffect來模擬類別型元件的生命週期方法
- 一個 Hook 處理三件事情: componentDidMount, componentDidUpdate, componentWillUnmount

----------------- 以下未整理完成
## 使用方法
1. 先 import 這個方法
2. 最基本的樣子 :
   useEffect(()=>{}, [])
3. ComponentDidMount

```javascript=
useEffect(()=>{
    //程式碼寫在這裡
}, [])
```

5.componentDidUpdate
ex. total 為改變的狀態

```javascript
useEffect(() => {
  //程式碼寫在這 在這邊會在componentDidMount&componentDidUpdate時執行
}, [total]);
```

- 如果只要在 update 時執行，要多一個狀態，來判斷是否完成 componentDidMount
- const [didMount, setDidMount] = useState(false)

作法一
1.

```javascript
useEffect(() => {
  console.log(componentDidMount);
  setDidMount(true);
}, []);
```

2.

```javascript
useEffect(() => {
  // 目的是加上條件，讓一開始在componentDidMount時不要執行，只有在update時候執行
  if (didMount) {
    console.log(componentDidUpdate);
  }
  // 在這邊會在componentDidUpdate時執行
}, [total]);
```

作法二
const [start, useStart] = useState(false)
在觸發事件中加上 setStart (true)

componentWillUnmount

沒有給陣列時，不管怎麼樣都會執行，大部分時候不會這樣子寫
useEffect(()=>{
    console.log('Parent的一部分')
})

類別型元件的componentDidUpdate
用來比較update前後差異，可以用在回到上一步
componentDidUpdate(prevProps, prevState){
    
}