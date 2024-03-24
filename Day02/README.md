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

## document
在 Web 開發中，window.document 是指當前窗口中的 HTML 文檔。它是一個 DOM 對象，代表整個 HTML 文檔的結構和內容。


### DOM: tree structure
Node(節點)有四種
- element
- text
- attribute
- document


## Event
BOM & DOM都有event，如上述BOM是針對瀏覽器視窗而DOM則是當前文件，而我真正想深入了解的事DOM event

### BOM 事件
BOM 事件是指發生在瀏覽器窗口或框架中的事件。它們與特定的 HTML 元素無關，而是與整個瀏覽器窗口或框架相關。

常見的 BOM 事件包括：

load：當瀏覽器完成加載網頁時觸發。
resize：當瀏覽器窗口或框架的大小發生更改時觸發。
scroll：當瀏覽器窗口或框架中的內容被滾動時觸發。
unload：當瀏覽器窗口或框架被關閉時觸發。
### DOM 事件
DOM 事件是指發生在 HTML 元素中的事件。它們與特定的 HTML 元素相關，例如按鈕、輸入框或圖像。

常見的 DOM 事件包括：

click：當用戶單擊 HTML 元素時觸發。
mouseover：當用戶的鼠標懸停在 HTML 元素上時觸發。
mouseout：當用戶的鼠標離開 HTML 元素時觸發。
keydown：當用戶按下鍵盤上的鍵時觸發。
keyup：當用戶鬆開鍵盤上的鍵時觸發。


# Event Object
所有的事件都是根據event object
事件也分為好幾類

| Object              | Handles                                    |
|---------------------|--------------------------------------------|
| AnimationEvent      | CSS animations                             |
| ClipboardEvent      | Modification of the clipboard              |
| DragEvent           | Drag and drop interaction                  |
| FocusEvent          | Focus-related events                       |
| HashChangeEvent     | Changes in the anchor part of an URL       |
| InputEvent          | User input                                 |
| KeyboardEvent       | Keyboard interaction                       |
| MouseEvent          | Mouse interaction                          |
| PageTransitionEvent | Navigation between web pages               |
| PopStateEvent       | Changes in the page history                |
| ProgressEvent       | The progress of loading external files     |
| StorageEvent        | Changes in the Web Storage                 |
| TouchEvent          | Touch interaction                          |
| TransitionEvent     | CSS transitions                            |
| UiEvent             | User interface interaction                |
| WheelEvent          | Mouse-wheel interaction                    |


> 事件列表可以參考這裡：https://www.w3schools.com/jsref/obj_events.asp

## Event Properties and Methods

- Properties: 
    - bubbles: Returns whether or not a specific event is a bubbling event
    `event.bubbles //true or false`
    - target: returns the element where the event occured.
    > 返回觸發事件的元素，例如: `<button>This is a button</button>`
    - type: Return the type of event that was triggered
- Methods:
    - stopPropagation(): 終止冒泡事件
        - [w3schools Demo](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_event_stoppropagation)

    - preventDefault(): 取消預設觸發行為
        - [w3schools Demo](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_event_defaultprevented)

### event.target
event.target已經是返回html element了，因此可以直接存取與修改元素的屬性
**例如：修改文件顏色**
```
<button style="color:blue" onclick="changeColor()">BUTTON</button>

<script>
function changeColor(){
    event.target.style.color = "red"
}
</script>
```


#### 補充01: event.target vs event.currentTarget
- Event.target: 返回觸發事件的element
- Event.currentTarget: 返回綁定事件監聽的element
[Demo: target v.s. currentTarget](./eventTargetDemo.html)

**預期結果**
1. 點outer: target返回outer; currentTarget返回outer
2. 點inner: target返回inner; currentTarget會返回outer & inner


#### 補充02: 冒泡事件 Event Bubbling 與 捕獲事件 Event Capturing
reference: https://www.explainthis.io/zh-hant/swe/fe-event-delegation-capture-bubble



