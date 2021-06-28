# Javascript event loop
### Philip Roberts JSConf EU 筆記 2021/05/24
*https://www.youtube.com/watch?v=8aGhZQkoFbQ*
> Question
> How does Callback work?
> What is single thread?

#### JS 是一種
- single threaded 單執行緒
- non-blocking 非阻塞
- asynchronous 非同步
- concurrent 並行 (基於event loop) *by MDN*

#### JS 有
- Call stack(呼叫堆疊)
- Event loop(事件循環)
- Callback queue(回調佇列)

V8引擎 是一個Chrome中的Runtime，其中包含了heap(記憶體) 和 call stack(呼叫堆疊)

JS Runtime 一次只能做一件事情，瀏覽器能夠同時做多件事情是因為**瀏覽器中不只有runtime而已**

> call stack is basically a data structure which records where in the programm we are.
>
> call stack 是一種資料結構，紀錄我們在程式中的哪個位置　ex. 在stack中放上東西，取下stack頂端的東西等等

#### Blocking 阻塞
若為同步時，stack被前面的工作給阻塞住，後面的工作就無法進行(必須等待完成後才能執行)
解決辦法：Async Callback(非同步回調)

#### JS 非同步回調的過程
當我們執行程式時，會把程式丟入stack中，執行後就從stack中移除，若該程式有callback function時，則會先傳給web API，經過等待時間，或由某個event觸發後，丟入queue(佇列)中，
event loop會檢查當stack清空時，將queue中的cb function傳入stack中執行。

- stack 像是堆疊起來的盤子，**先進後出**
- task queue 就像是在排隊的工作，**先進先出**
- event loop像是一個指揮官，會檢查stack，如果stack空了的時候，就會讓按照進入隊伍的順序，把工作丟回去stack當中

如果function中又呼叫了其他的function則會按照呼叫的順序由下至上堆疊至stack中
當我們return回傳時，就從stack中移除了該程式碼 


**setTimeout**不是保證執行時間，而是保證**最短的等待執行時間**
因為包含了setTimeout這個callback function的函式會先被執行，然後將cb丟給web API，經過等待時間後，再放入queue，event loop會在stack空了以後將cb丟進stack中執行

為了避免UI的體驗差，應該要避免程式在stack中的停留時間太長，例如載入大量的動畫和圖片，否則在queue中等待的callback function就無法被執行
