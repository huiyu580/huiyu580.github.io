# 狀態
## 狀態為陣列時
1. 先從目前狀態拷貝一份(因為狀態值
immutable)
2. 在拷貝出來的陣列或物件上更新
3. 把更新完成後的陣列或物件，設定回原本狀態中
```javascript=
const setProdocutItemCount = (productIndex, newCount) => {

    const newCounts = [...counts]

    newCounts[productIndex] = newCount

    setCounts(newCounts)
}
```