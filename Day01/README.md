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
瀏覽器***從上到下***的次序來執行程式碼。通常我們都會把JavaScript檔案放在`</body>`前面，當瀏覽器跑完前面的HTML程式碼，才去跑JavaScript的檔案：
```
<body>
    <!-- HTML程式碼 -->
    <script src="index.js"></script>
</body>
```

#### Demo
1. 非引入式的script會先執行，畫面文字都看不到: [demo](https://iamlaurenwang.github.io/js30Demo/Day01/renderOrder03.html)
> 解決辦法：使用window.onload或是其他前端框架api(如jQuery中的ready()): [demo](https://iamlaurenwang.github.io/js30Demo/Day01/renderOrder04.html)
2. 引入式script放在HTML程式碼***之前***，會先執行JS腳本: [demo](https://iamlaurenwang.github.io/js30Demo/Day01/renderOrder01.html)
3. 引入式script放在HTML程式碼***之後***，會先顯示畫面文字: [demo](https://iamlaurenwang.github.io/js30Demo/Day01/renderOrder02.html)


# event.target
# window
# document