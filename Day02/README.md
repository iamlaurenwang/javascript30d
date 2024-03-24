# window, document, event
Day2針對以上幾個在開發時，常常用到的指令做更深入的理解


## window
> The window object represents an open window in a browser.
Window物件是瀏覽器全局物件，它代表瀏覽器視窗。
window物件包含屬性及方法，可用於控制瀏覽器視窗

### 屬性
- location：獲取或設定瀏覽器視窗的網址
- history：獲取瀏覽器視窗的瀏覽歷史記錄
- document：獲取瀏覽器視窗的HTML文件
- navigator：獲取有關瀏覽器和作業系統的資訊
- screen：獲取有關螢幕的資訊

[w3schools:The Window Object](https://www.w3schools.com/jsref/obj_window.asp)
### 方法
- alert()：顯示一個警示訊息
- confirm()：顯示一個確認訊息
- prompt()：顯示一個輸入訊息的對話框
- open()：開啟一個新的瀏覽器視窗
- close()：關閉瀏覽器視窗
- setInterval()
- setTimeout()
- clearInterval()
- clearTimeout()

#### 補充01： 取得瀏覽器作業系統資訊
1. 使用者的瀏覽器資訊: `navigator.appName`
2. 偵測使用plugin: AdBlock
    - 使用 Chrome 擴充套件 API
    - 使用第三方庫來檢測 Chrome 擴充套件是否已安裝: chrome-extension-detector


#### 補充02: 使用瀏覽器原生popup注意事項
1. 原生popup出現會導致瀏覽器運行的停止，直到使用者點確認或取消才會繼續運行
> It’s worth reiterating again that these methods will stop the execution of a program in its tracks. This means that everything will stop processing at the point the method is called, until the user clicks OK or Cancel. This can cause problems if the program needs to process something else at the same time or the program is waiting for a callback function.
[reference](https://www.sitepoint.com/javascript-window-object/)

2. prompt可能有被XSS攻擊的疑慮
範例：
```
<script>
function promptUser() {
  var input = prompt("請輸入您的姓名");
  alert(input);
}
</script>

<button onclick="promptUser()">輸入姓名</button>
```

- 如果攻擊者點擊“輸入姓名”按鈕，並輸入以下內容：`<script>alert("XSS 攻擊成功！");</script>`


- 為了防止 XSS 攻擊，可以使用以下措施：
    1. 對使用者輸入進行驗證
    2. 使用輸出編碼
    3. [使用 HTTP 內容安全策略 (CSP)](https://www.tsg.com.tw/blog-detail10-317-0-content-security-policy.htm)
        > 　簡單來說，CSP 是瀏覽器提供設定白名單的機制，網站會告訴瀏覽器那些網頁的哪些位置可以連、哪些位置不能連，並且目前大部分的瀏覽器都能支援 CSP。

