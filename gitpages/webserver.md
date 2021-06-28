# 2021/06/06 小賴老師上課筆記

## Web server (express, express generator)

### 用 Node JS 架設簡單的 web server

- 使用 node JS 內建的 package

```javascript
const http = require("http");
```

- 建立 server 物件

```javascript
const server = http.createServer();
```

- 使用 server 物件裡的 listener 函式來處理 request 和 response(此時還沒有連線)
- 需回覆的有：status code (2xx, 3xx, 4xx, 5xx)

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
  switch (path) {
    case "/":
      res.write("首頁");
      res.end("停止response process");
      break;
    case "/about":
      res.end("關於我們");
      break;
    case "/contact":
      res.end("聯絡我們");
      break;
  }
});
```

- 連線並設定 port

```javascript
// 連線至localhost:3000
server.listen(3000, () => {
  console.log("我跑起來了，我要收 3000 Port");
});
```

### 用 express 架設 web server

- 安裝 express package

```bash
npm init -f
npm i express
```

- 導入 express

```javascript
const express = require("express");
```

- 利用 express 建立一個 express application

```javascript
let app = express();
```

- middleware 中間件 中介函式

  - 在 express 中 req -> middlewares... -> router
    可以透過 middlewares 幫你處理進入 router 前的其他工作
  - 可以指定特定路由經過這個中間件
  - example: 登入才可以訪問的網頁
  - 因中間件有很多個，要加上`next()`，才會繼續往下處理
  - example: 處理訪問時間

  ```javascript
  app.use(function (req, res, next) {
    let current = new Date();
    console.log(`有人來訪，在${current}`);
    next();
  });
  ```

- 處理路由 express 由上而下，找到之後就不會再往下找

```javascript
app.get("/", function (req, res) {
  res.send("Hello, express");
});
app.get("/about", function (req, res) {
  res.send("About express");
});
app.get("/test", function (req, res) {
  res.send("Express test page");
});
app.post("/contact", function (req, res) {});
```

- Listener

```javascript
app.listen(3000, () => {
  console.log("我跑起來了");
});
```

- 不需要額外去除 URL 中的 query string

### express generator (應用程式產生器)

- 安裝 express-generator 在 global，然後建立 my-web 資料夾

```bash
npm i -g express-generator
npx express --view=pug my-web
```

### 補充:

#### 使用 package nodemon 協助，不需要每次 ctrl+c 重啟，只要存檔時就會重啟。因是所有專案皆可使用的工具，建議安裝在全域

    1. `npm i -g nodemon`
    2. 把package.json 中的script新增`"dev": "nodemon server.js"`
    3. `npm run dev`

#### 建立快捷鍵

在 package.json 中的 script 增加 `"dev": "node server.js"`，指定 dev 為 node server.js，之後就可以在 terminal 用`npm run dev`來執行 server.js

#### 用`npm init -f` 將專案交給 npm，快速建立 package.json

#### module, package, framework 的差別

- module < package < framework
- express 是 package，但完整到足以被稱為框架

### 參考資料

[解析與處理 url 的參數](https://pjchender.blogspot.com/2018/08/js-javascript-url-parameters.html)
[express 文件](http://expressjs.com/en/starter/hello-world.html)
[express generator](https://expressjs.com/zh-tw/starter/generator.html)
