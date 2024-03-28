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
1. 複製陣列
    - 深拷貝
    - 淺拷貝
    - concat
2. 判斷是否包含某個值
    - indexOf
    - includes

3. 陣列內容處理
    - forEach
    - filter
    - reduce
4. 分類 (sort)
5. 字串&陣列: https://developer.mozilla.org/zh-TW/docs/Learn/JavaScript/First_steps/Arrays#%E5%9C%A8%E5%AD%97%E4%B8%B2%E8%88%87%E9%99%A3%E5%88%97%E4%B9%8B%E9%96%93%E8%BD%89%E6%8F%9B


// valuesOf
// slice
// join
// pop
// shift
// push
// some, every
 ### array v.s set