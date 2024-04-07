## Closure閉包
closure和作用域相關，一般來說全域變數(Global Variables)可以在`function`中存取，但是在`function`中宣告的變數只能在`function`中存取

### 變數生命週期
- 全域變數在網頁關閉或跳到下一頁時，生命週期結束
- 本地變數生命週期短，在函式觸發後生命週期開始，函式結束後生命週期也隨之結束



### 創建closure要點
closure可以讓function擁有private variable(私有變數)


1. function中要return另一個function
```
function func(){
    return closureFunc(){
        // 形成閉包
    }
}
```

2. 另外宣告變數，存取私有變數
```
let closureVar = func(); // func這時候已經拿到返回的closureFunc()
```

3. 應呼叫私有變數function: `closureVar()`


reference:
1.  [深入淺出 JavaScript 閉包（closure）](https://pjchender.dev/javascript/js-closure/)
2. [JavaScript基本功修練：Day23 - 閉包](https://ithelp.ithome.com.tw/articles/10250925)