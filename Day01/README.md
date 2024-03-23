# 瀏覽器與JavaScript

## JavaScript基本功修練
在瀏覽器上使用JavaScript能夠為網頁加入互動元素，與使用者進行互動。
> 換言之，JavaScript就是能夠把靜態網頁動起來。

### Client Side JavaScript 限制
為了保障使用者安全及隱私，在客戶端瀏覽器的JavaScript沒法做以下的事：
1. 讀取、存取、執行、複製user電腦中的檔案
- 例如：請user上傳文件
- 解決辦法： 利用form submit or ajax 上傳到後端

2. 直接控制作業系統或硬體
- 例如：JavaScript不能直接關閉電腦 or 執行本機中的檔案(.exe)

3. 跨域存取（Cross-Origin Requests）
> 不能操控其他域名不同的網頁，也不能提取它的資料。即使使用者的瀏覽器同時開啟多個網頁，它們之間都不能干涉對方，提取對方在伺服器的資料。


### 渲染順序
瀏覽器**從上到下**的次序來執行程式碼。通常我們都會把JavaScript檔案放在`</body>`前面，當瀏覽器跑完前面的HTML程式碼，才去跑JavaScript的檔案：
```
<body>
    <!-- HTML程式碼 -->
    <script src="index.js"></script>
</body>
```

#### Demo
1. 非引入式的script會先執行，畫面文字都看不到: [demo](https://iamlaurenwang.github.io/js30Demo/Day01/renderOrder03.html)
> 解決辦法：使用window.onload或是其他前端框架api(如jQuery中的ready()): [demo](https://iamlaurenwang.github.io/js30Demo/Day01/renderOrder04.html)
2. 引入式script放在HTML程式碼**之前**，會先執行JS腳本: [demo](https://iamlaurenwang.github.io/js30Demo/Day01/renderOrder01.html)
3. 引入式script放在HTML程式碼**之後**，會先顯示畫面文字: [demo](https://iamlaurenwang.github.io/js30Demo/Day01/renderOrder02.html)


# JavaScript Engine
在瀏覽器上執行JavaScript時，需要透過瀏覽器本身附帶的**JavaScript的引擎**去進行解讀。

| Engine    | Browser |
| -------- | ------- |
| V8  | Chrome    |
| SpiderMonkey  | Firefox    |
| JavaScriptCore  | Safari    |
| Chakra  | Edge    |

- V8是Google開發的JavaScript引擎，它也是目前最快的JavaScript引擎之一。
V8使用JIT（即時編譯）技術將JavaScript程式碼轉換為機器碼，這可以顯著提高執行效率。

- SpiderMonkey是Mozilla基金會開發的JavaScript引擎，它也是歷史最悠久的JavaScript引擎之一。
SpiderMonkey使用TraceMonkey和IonMonkey等技術來提高JavaScript的執行效率。

- JavaScriptCore是蘋果公司開發的JavaScript引擎，它也是WebKit瀏覽器引擎的核心組件。
JavaScriptCore使用JIT技術將JavaScript程式碼轉換為機器碼。

- Chakra是微軟公司開發的JavaScript引擎，它也是Edge瀏覽器的核心組件。
Chakra使用JIT技術將JavaScript程式碼轉換為機器碼。


### JavaScript如何在瀏覽器運作？

JavaScript普遍被介定為直譯型語言，而非編譯型，當我們寫完一段JavaScript後，並不會馬上進行編譯，而是把我們寫和看得懂的JavaScript（高階語言），一行一行地被轉成機器看得懂的語言（低階語言），並且執行。

- 編譯型(Compiled language)：
程式碼在被執行前，整個程式碼會先被編譯器轉成機器語言，再拿去執行。若程式碼有錯，在預先編譯的過程中會報錯，而程式不會被執行。例子：Java，C++。
- 直譯型(Interpreted language)：
程式碼一行一行被執行，並一行一行轉成機器語言，整個過程是一邊執行一邊進行編譯。若程式碼有錯，程式碼仍然會被執行，執行後才會回報錯誤。例子：Python，PHP。

在編譯上，JavaScript省去了先編譯後執行的動作，但在顯示速度上，**當處理大量JS程式碼時，直譯型會比編譯型慢**。

#### 引擎編譯流程
![JavaScript編譯流程](https://i.imgur.com/kSGCP16.png)


1. 語法分析器（Parser）
JavaScript的程式碼會被轉為一堆UTF-16字符編碼，再把它解析成一個個字詞，分辨它們之間的關係。
> 可以參考Esprima(開源JavaScript編譯器): https://esprima.org/demo/parse.html#

2. 抽象語法樹（AST）
根據tokens組成抽象語法樹，用樹狀去表現當中的結構和關係，並用一個個節點的形成顯示出來。
![抽象語法樹](https://i.imgur.com/0MkHass.png)

3. 直譯器（Interpreter）
直譯器會根據AST結構，產生byte code，讓機器看得懂。
當byte code生成後，這時候機器已經能夠用byte code來執行程式，**而之前產生的AST就會被刪掉，省回記憶體空間**。

4. 性能分析（Profiler）+ 優化編譯器（Compiler）
雖然這個階段可依靠byte code來執行程式，但**效能仍然是很低**。因為當機器面對大量重複同一動作程式碼，例如有一個function負責把兩個數字相加，但它要重複跑100次，如果按之前的做法，以上流程便要跑100次，這樣效能會很低。

所以，這時候優化編譯器就會透過性能分析，檢視和計算有沒有重複次數很大的機器碼，如有的話，它便會假設你之後都會想重複這個動作，於是幫你優化成更精簡的機器碼並且儲存。

> **如果發現優化程式碼的假設不成立，引擎會返回直譯器，產生新的byte code。**
> 由於JavaScript容許隨時更改型別和值，因此之前在優化前，即是性能分析及優化編譯器過程中，所定立的假設就會不成立，這時候便要重返直譯器產生新的byte code。




references
[JavaScript基本功修練：Day2 - 瀏覽器與JavaScript引擎](https://ithelp.ithome.com.tw/articles/10238495)

[淺淡 JS Engine 機制](https://medium.com/walkout/%E6%B7%BA%E6%B7%A1-js-engine-%E6%A9%9F%E5%88%B6-77391b4dd3db)