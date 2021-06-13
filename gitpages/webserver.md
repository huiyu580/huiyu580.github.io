# 2021/06/06 小賴老師上課筆記
## Web server (express, express generator)

### 用Node JS架設簡單的web server
- 使用node JS 內建的package
```javascript
const http = require("http");
```

- 建立server物件
```javascript
const server = http.createServer();
```

- 使用server物件裡的listener函式來處理request和response(此時還沒有連線)
    - 需回覆的有：
        status code (2xx, 3xx, 4xx, 5xx)
```javascript
const server = http.createServer((req, res) => {
    // 使用 req請求物件 和 res回覆物件 來處理連線
    // 設定status code
    res.statusCode = 200;
    // 能夠顯示中文
    res.setHeader("Content-Type", "text/plain;charset=UTF-8");

    // 先處理url，移除query string，非必要結尾斜線，改成小寫等等
    const path = req.url.replace(/\/?(?:\?.*)?$/, "").toLocaleLowerCase();

    // 判斷url給出不同的response
    switch(path) {
        case "/":
            res.write("首頁")
            res.end("停止response process")
            break;
        case "/about":
            res.end("關於我們")
            break;
        case "/contact":
            res.end("聯絡我們")
            break;
        
    }
});
```
- 連線並設定port
```javascript
// 連線至localhost:3000
server.listen(3000, () => {
    console.log("我跑起來了，我要收 3000 Port")
});
```

### 用express架設web server

- 安裝express package
```bash
npm init -f
npm i express
```

- 導入express
```javascript
const express = require("express")
```

- 利用express建立一個express application
```javascript
let app = express();
```

- middleware 中間件 中介函式
    - 在express中 req -> middlewares... -> router
    可以透過 middlewares 幫你處理進入router前的其他工作
    - 可以指定特定路由經過這個中間件
    - example: 登入才可以訪問的網頁
    - 因中間件有很多個，要加上`next()`，才會繼續往下處理
    - example: 處理訪問時間
    ```javascript
    app.use(function(req, res, next){
        let current = new Date();
        console.log(`有人來訪，在${current}`)
        next(); 
    })
    ```

- 處理路由 express 由上而下，找到之後就不會再往下找
```javascript
app.get("/", function(req, res){
    res.send("Hello, express")
});
app.get("/about", function(req, res){
    res.send("About express")
});
app.get("/test", function(req, res){
    res.send("Express test page")
})
app.post("/contact", function(req, res){});
```

- Listener
```javascript
app.listen(3000, () => {
    console.log("我跑起來了")
})
```

- 不需要額外去除URL中的query string

### express generator (應用程式產生器)
- 安裝express-generator在global，然後建立my-web資料夾
```bash
npm i -g express-generator
npx express --view=pug my-web
```

### 補充: 
#### 使用package nodemon協助，不需要每次ctrl+c重啟，只要存檔時就會重啟。因是所有專案皆可使用的工具，建議安裝在全域
    1. `npm i -g nodemon`
    2. 把package.json 中的script新增`"dev": "nodemon server.js"`
    3. `npm run dev`
#### 建立快捷鍵
在package.json中的script增加 `"dev": "node server.js"`，指定 dev 為 node server.js，之後就可以在terminal用`npm run dev`來執行server.js

#### 用`npm init -f` 將專案交給npm，快速建立package.json

#### module, package, framework的差別
- module < package < framework
- express 是 package，但完整到足以被稱為框架

### 參考資料
[解析與處理url的參數](https://pjchender.blogspot.com/2018/08/js-javascript-url-parameters.html)
[express文件](http://expressjs.com/en/starter/hello-world.html)
[express generator](https://expressjs.com/zh-tw/starter/generator.html)
