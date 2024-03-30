## array
 1. 創建陣列方法
 - const arr = []
    - 也可以直接塞資料進去: `const arr = [ 1, 2, 3 ]`

- Array Constructor 陣列建構子 `const arr = new Array()`
    - 可以預先定義陣列長度:  `const arr = new Array(3)`
    - 也可以加入值: `const arr = new Array(1,2,3)`

2. 取得陣列資料
- 使用index: 以下兩個方法若找不到這個index都會返回undefined
    - `arr[0]`
    - `arr.at(0)`
        - 使用at的優點: 可以接受負數
        - `arr.at(-1)`: 返回最後一個值
        - 不過目前僅有較新版本瀏覽器支援
        > Since March 2022, this feature works across the latest devices and browser versions. This feature might not work in older devices or browsers.


3. 判斷是否為陣列
    - Array.isArray()
        - return Boolean

### 清空陣列方法
1. 給空陣列: `arr = []`
    - 給了另一個記憶體位置到 arr

case 01
```
const arr = [ 1, 2, 3 ] //Heap中有一組資料被指向stack中的arr
arr = [] //重新讓stack的arr指向Heap的另一個地址(資料)
```
因為GC的機制，`[1,2,3]`就會被回收

**case 02**
``` 
let data = [1,2,3]
data2 = data
data = []
console.log(data2) //[1,2,3]
console.log(data) //[]
```

2. 將陣列的 length 屬性設為 0
    - 缺點: 會影響到原始資料

```
let arr1 = [1, 2, 3, 4, 5, 6];
let arr2 = arr1;
arr1.length = 0;

console.log(arr1) // []
console.log(arr2) // []
```

3. splice()
- 會修改到原始資料
```
const fruits = ["Banana", "Orange", "Apple", "Mango", "Kiwi"];

fruits.splice(0, fruits.length);
```

### Array常用methods
![常見 Array 方法](https://ithelp.ithome.com.tw/upload/images/20190905/20106426psTRBiwFBt.png)

1. 複製陣列
    - 深拷貝
    - 淺拷貝
    - concat

2. [搜尋](https://www.w3schools.com/js/js_array_search.asp)
    - indexOf(): 搜尋陣列並返回找到的**第一個**元素位置，找不到會返回-1
    - lastIndexOf(): 搜尋陣列並返回找到的**最後一個**元素位置，找不到會返回-1
    - includes(): 返回Boolean
        - ES6 
        - 不支援Edge 13和更早版本
    - find(): 利用條件，返回第一個符合的元素
        - ES6
    ```
    const numbers = [4, 9, 16, 25, 29];
    let first = numbers.find(myFunction);

    function myFunction(value, index, array) {
    return value > 18;
    }

    console.log(first) //25
    ```

3. 陣列各項內容處理
    - forEach
    - filter
    - reduce


4. [分類 (sort)](https://www.w3schools.com/js/js_array_sort.asp)
    - sort預設分類**字串**，例如: a>b>c
    - 數字的排列需要加上compare function: 
    ```
    const points = [40, 100, 1, 5, 25, 10];
    points.sort(function(a, b){return a - b});
    ```

5. 字串&陣列: https://developer.mozilla.org/zh-TW/docs/Learn/JavaScript/First_steps/Arrays#%E5%9C%A8%E5%AD%97%E4%B8%B2%E8%88%87%E9%99%A3%E5%88%97%E4%B9%8B%E9%96%93%E8%BD%89%E6%8F%9B
    - join(): 將陣列（或一個類陣列（array-like）物件 (en-US)）中所有的元素連接、合併成一個字串，並回傳此字串。
    ```
    const elements = ['Fire', 'Air', 'Water'];

    console.log(elements.join());    // Expected output: "Fire,Air,Water"

    console.log(elements.join(''));    // Expected output: "FireAirWater"

    console.log(elements.join('-'));    // Expected output: "Fire-Air-Water"
    ```
6. 首尾相關method
    - shift(): **移除**並回傳陣列第一個元素
        ```
        const array1 = [1, 2, 3];

        const firstElement = array1.shift();

        console.log(array1);    // Expected output: Array [2, 3]

        console.log(firstElement);    // Expected output: 1
        ```
    - unshift(): **添加**一個或多個元素至陣列的開頭，並且<ins>回傳陣列的新長度</ins>。
        ```
        const array1 = [1, 2, 3];

        console.log(array1.unshift(4, 5));   // Expected output: 5
        console.log(array1);    // Expected output: Array [4, 5, 1, 2, 3]
        ```
    - pop(): **移除**並回傳陣列的最後一個元素
        ```
        const plants = ['broccoli', 'cauliflower', 'cabbage', 'kale', 'tomato'];

        console.log(plants.pop());  // Expected output: "tomato"
        console.log(plants);    // Expected output: Array ["broccoli", "cauliflower", "cabbage", "kale"]
        ```
    - push(): **添加**一個或多個元素至陣列的末端，並且<ins>回傳陣列的新長度</ins>。
        ```
        const animals = ['pigs', 'goats', 'sheep'];

        const count = animals.push('cows');
        console.log(count);         // Expected output: 4
        console.log(animals);        // Expected output: Array ["pigs", "goats", "sheep", "cows"]
        ```

7. 合併陣列
    - 淺拷貝方法
        1. slice()
        2. concat()




// valuesOf
// slice
// join
// some, every


### 淺拷貝
![shallow copy](https://miro.medium.com/v2/resize:fit:640/format:webp/1*xrqXUJ_WZBmIDLORwKJj7A.png)
- 共用同個記憶體空間

```
let obj1 = {a: {a: 1}}
let obj2 = {a: obj1.a}
obj1.a.a = 2
console.log(obj2.a)   // 輸出{a: 2}而不是{a: 1}
```
這時候 obj2 內的值也變了，所以我們可以發現，**只要物件超過一層**，這種作法只會複製表層而已，深層的內容還是共用同一個記憶體，因此兩者還是會互相影響。
> $\textcolor{red}{\textsf{在Vue2中的響應式就有此問題}}$	

Object copy using spread syntax actually shallow or deep?
> Now, what a spread operator does? It deep copies the data if it is not nested. For nested data, it deeply copies the topmost data and shallow copies of the nested data.
https://stackoverflow.com/questions/61421873/object-copy-using-spread-syntax-actually-shallow-or-deep

關於JS中的淺拷貝(shallow copy)以及深拷貝(deep copy)
https://medium.com/andy-blog/%E9%97%9C%E6%96%BCjs%E4%B8%AD%E7%9A%84%E6%B7%BA%E6%8B%B7%E8%B2%9D-shallow-copy-%E4%BB%A5%E5%8F%8A%E6%B7%B1%E6%8B%B7%E8%B2%9D-deep-copy-5f5bbe96c122


 ## [Set](https://ithelp.ithome.com.tw/articles/10214228)
 - ES6語法
 - 集合，不能放重複的資料

 ### Set methods
 - add()
 - delete()
 - has()
 - clear()
 - values()

### Set properties
- size: 此集合裡有幾個元素


### Set轉為陣列
1. 使用spread operator
```
let data = new Set();
data.add(1)
data.add(20)

console.log(Array.isArray([...data]) ) // true
```

2. Array.from()
```
let data = new Set();
data.add(1)
data.add(20)

console.log(Array.isArray(Array.from(data))) //true
```

### [Set & Array](https://ithelp.ithome.com.tw/articles/10214361)
