## THIS
### [MDN解釋](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)
> The `this` keyword refers to the context where a piece of code, such as a function's body, is supposed to run.
也就是說，`this`代表一段要執行的程式的環境

- context in programming
 In programming, the term "context" refers to the **circumstances or environment** in which a particular piece of code or a function is executed.

 > The value of `this` in JavaScript depends on how a function is invoked (runtime binding), not how it is defined.
 `this`的值是根據函式如何被觸發的，而不是函式怎麼定義的

例如:
> When a regular function is invoked as a method of an object (obj.method()), this points to that object. When invoked as a standalone function (not attached to an object: func()), this typically refers to the global object (in non-strict mode) or undefined (in strict mode). 
1. 普通函式在物件中，這時的`this`指向物件本身
2. 獨立存在的函式，`this`則指向global object(window)或是`undefined`

> Arrow functions differ in their handling of this: they inherit this from the parent scope at the time they are defined. This behavior makes arrow functions particularly useful for callbacks and preserving context. However, arrow functions do not have their own this binding. Therefore, their this value cannot be set by bind(), apply() or call() methods, nor does it point to the current object in object methods.

箭頭函式`this`的指向是繼承父層作用域，自己本身沒有`this`
適用箭頭函式時機:
1. callback
2. 維護執行環境



 > $\textcolor{red}{\textsf{}}$	

### 物件中的this
```
const obj = {
    num: 10,
    func: function(){
        return this.num
    }
}

console.log(obj.func()) //10
```

### Standalone Function 獨立存在的函式
```
function func(){
    console.log(this)
}

func() //[object Window]
```

### 補充: event中的this
DOM事件中的this會指向DOM元素本身

```
<body>
<button id="btn">BUTTON</button>
<script>
let btn = document.getElementById('btn')

btn.addEventListener('click', function(){
	console.log(this) // <button id="btn">BUTTON</button>
})

</script>
</body>
```

## Context 執行環境
> The value of this depends on in which context it appears: function, class, or global.

### Function context
根據函式被觸發方式，`this`會有所不同

case 1: 一般function
```
function func(){
    return this;
}

console.log(func()) //window object
```

case 2: object中的function
```
// 1. 先寫一個一般function
function func(){
    return this;
}

// 2. 創建物件
const obj = { name: "obj" };

// 3. 將物件加上function
obj.func = func;

//4. 呼叫物件中的function
console.log(obj.func()) // { name: "obj", func: [Function: func] }
```


### Overall
| context | result |
|---|---|---|
| Object中的一般function | Object本身 | 
| 一般function | Global Window Object | 
| DOM事件 | DOM元素 | 
| callbacks | Global Window Object | 
| 箭頭函式 | 根據context而定 | 






reference:
1. [JavaScript基本功修練：Day20 - this的運作](https://ithelp.ithome.com.tw/articles/10249601)
2. [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this#examples)
3. [The JavaScript this Keyword](https://www.w3schools.com/js/js_this.asp)


