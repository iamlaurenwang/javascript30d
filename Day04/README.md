## primitive type 基本型別
當一個變數被賦予基本型別的值時，整個值就會存在記憶體裏。
一般來說存放在Stack中
當我們要拷貝基本型別的值到另一個變數，我們只會拷貝它們的值，**而該兩個變數並不會影響到對方**。這個情況稱為傳值(pass by value)。
```
var box1 = 10;
var box2 = 'hello';

//拷貝box1,box2的值
var boxA = box1;
var boxB = box2;

boxA = 30;
boxB = 'goodbye';

console.log(box1,box2,boxA,boxB) // 10,"hello",30,"goodbye"
```
### Stack
![Stack](https://felixgerschau.com/static/b94165593eb6e02d73039d8b2cfccfdd/5a190/stack-memory-explained.png)

## object types 物件型別
但物件型別的存取方法就不同了。當變數被賦予的是物件型別的資料，**記憶體會存放該物件在記憶體中的地址，並引用該地址來指向該物件**。
如果變數的值是物件型別，棧內存(stack)會存放該物件在堆內存(heap)的地址，並引用該地址來指向該存放在堆內存(heap)的物件。
所以，當我們要拷貝一個物件到另一個變數時，我們拷貝的是該物件的地址，換言之，如果物件有被修改，所有引用該物件地址的變數，它們的值都會被修改。
### Heap
![Heap](https://felixgerschau.com/javascript-memory-management/)




## 記憶體生命週期
- 分配-使用-釋放
    1. 分配程式需要用到的記憶體空間
    2. 使用分配到的記憶體空間（讀寫操作）
    3. 當不會再使用時要釋放被配置的記憶體空間

### JS Engine記憶體分配
**ram and browser**
使用瀏覽器會占用RAM(電腦內存)，browser將內存分配給HTML,CSS渲染,HTTP request, JS Engine
javascript中的物件型別資料，就是在JS引擎中發生

- RAM(電腦分配給瀏覽器的內存)
    - Code Space 代碼空間 => 儲存變數
    - Data Space 數據空間 => 儲存資料
        - Stack: Primitive Type
        - Heap: Reference Type
            - new space
                - 存活時間較短的物件
                - 垃圾回收的速度會比較快
                - 空間卻比較小大概只有 1–8 MB 左右
                - 存在 New Space 中的物件也被稱作 Young Generation
            - old space
                - 存活時間較久的物件
                - 這些物件是在 New Space 中經過幾次 GC Cycle 並成功存活後才被移到 Old Space，
                - 垃圾回收的效率比較差，因此它執行 GC 的頻率相較於 New Space 會比較低
                - 在 Old Space 中的物件也被稱作 Old Generation。
![structure tree](https://miro.medium.com/v2/resize:fit:720/format:webp/1*JwkWC-SlF4hbvyZJP33duQ.png)

範例: 

```
const str = "hello"
```
str => code space
"hello" => data space/stack

### 執行環境Execution Context
當執行一段 JavaScript 的程式碼時需要先經過編譯，並創建所謂的執行環境（Execution Context）， 接著再按照順序執行程式碼。
```
function ironman(){
    let one = "鐵人賽";
    let two = one;
    let three = { author: "Kyle Mo"};
    let four = three;
}
ironman();
```
!(executionContext)[https://miro.medium.com/v2/resize:fit:720/format:webp/1*w2zK9HrlgQIoDQm4XhXs-Q.png]


#### 為什麼不把所有數據存到 Stack 裡就好？
原因是 JS Engine 是透過 stack 來維護 Execution Context 的切換狀態，如果 Stack 太過肥大，會影響 Context Switch 的執行效率，連帶影響到整個程式執行的效率。

### Garbage Collection垃圾回收機制
Garbage Collector （簡稱 GC）的工作是「追蹤記憶體分配的使用情況，以便自動釋放一些不再使用的記憶體空間」。
了解 GC 基本的運作方式是很重要的，有了基本的觀念才能避免 memory leak 的發生，讓應用的效能不會因為記憶體空間不足而出現瓶頸甚至崩潰。
- new space(Young generation): Scavenge collection
- old space(Old generation): Mark-Sweep collection




reference: 
1. [JavaScript基本功修練：Day6 - 傳址、傳值](https://ithelp.ithome.com.tw/articles/10241346)
2. [了解瀏覽器的棧內存 (Stack) ＆ 堆內存 (Heap)](https://roykwokcode.medium.com/%E6%99%AE%E9%80%9A%E9%A1%9E%E5%9E%8B%E5%92%8C%E5%B0%8D%E8%B1%A1%E7%9A%84%E5%8D%80%E5%88%A5-%E6%A3%A7%E5%85%A7%E5%AD%98-stack-%E5%A0%86%E5%85%A7%E5%AD%98-heap-44295724848c) => 推推推
3. [Day26 X Memory Management In JavaScript](https://ithelp.ithome.com.tw/articles/10280288) => 很深入
4. [JavaScript's Memory Management Explained](https://felixgerschau.com/javascript-memory-management/) => 英文版，圖片、動畫，詳細


## 補充
### extra: 深淺拷貝

基本型別:賦值 => 深拷貝
物件型別:因存在引用關係，會有深淺拷貝問題


### extra: memory leak 記憶體流失
像是 C/C++ 這類的語言需要開發者自己手動管理記憶體的釋放，而 Java 或 JavaScript 這類有垃圾回收機制的語言則不用手動釋放記憶體，但是不要以為這樣就安全了，在開發時有些寫法會造成垃圾回收機制沒辦法正確判斷記憶體已經不再被使用了，而無法被自動會收，造成所謂的 Memory Leak。

在 JavaScript 中，遵守某些 Best Practices 或是避免一些寫法可以盡量避免 Memory Leak 的發生。

#### [Global variables全域變數](https://felixgerschau.com/javascript-memory-management/#global-variables)
> Storing data in global variables is probably the most common type of memory leak.
- 使用`var`宣告變數，JavaScript Engine會自動將變數提升為`window`Object
- 函式以function開頭定義，也會被提升為`window`Object
```
//All three variables, user, secondUser, and getUser, will be attached to the window object.

user = getUser();
var secondUser = getUser();
function getUser() {
  return 'user';
}

```
##### Solution
- 程式運行在`strict mode`，可以避免這個問題
- 避免將變數宣告在`root`
- 如果真的要宣告在`root`，當不再需要使用這個資料時，記得釋放記憶體，分配null給這個全域變數 => `user = null`

#### [Timer & Callbacks](https://felixgerschau.com/javascript-memory-management/#forgotten-timers-and-callbacks)
timer和callback可能導致應用程式記憶體用量提升，尤其是在SPA中，使用上需要特別注意

- timer
```
const object = {};
const intervalId = setInterval(function() {
  // everything used in here can't be collected
  // until the interval is cleared
  doSomething(object);
}, 2000);
```

範例程式中的object不會被回收，因為interval從未被清除:
` clearInterval(intervalId) `

> 這在SPA中尤其重要。在切換頁且需要使用到計時功能，若不清除，interval會在背景持續執行

- callbacks: 這在現今的瀏覽器不再是個問題，在過去，舊瀏覽器需要移除eventListener

### 如果瀏覽器發生memory leak，會出現甚麼畫面或結果?

瀏覽器發生記憶體洩漏時，可能會出現以下畫面或結果：
- 瀏覽器速度變慢
- 瀏覽器變得不穩定，容易崩潰
- 瀏覽器佔用大量記憶體，導致系統資源不足
- 系統出現錯誤訊息

具體的畫面或結果取決於記憶體洩漏的嚴重程度。如果記憶體洩漏很小，可能只會導致瀏覽器速度變慢。如果記憶體洩漏很大，可能導致瀏覽器崩潰或系統死機。

以下是一些常見的記憶體洩漏症狀：
- 瀏覽器在開啟大量分頁或使用大量資源的網站時，速度變慢
- 瀏覽器在使用某些擴充功能或外掛程式時，變得不穩定
- 瀏覽器在執行某些操作時，佔用大量記憶體
- 系統出現「記憶體不足」的錯誤訊息

如果遇到上述情況，可以嘗試以下方法來解決：
- 重啟瀏覽器
- 關閉不使用的分頁和擴充功能
- 更新瀏覽器到最新版本
- 檢查系統是否有其他程式正在佔用大量記憶體