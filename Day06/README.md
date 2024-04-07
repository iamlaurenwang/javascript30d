## Intro
在JavaScript中，幾乎所有東西都是Object
1. 用`new`定義的東西都是Object
2. Array, function都是Object

### JavaScript Primitives基本型別
基本型別資料不會有property或是method，在JavaScript中，有7種基本型別資料:
1. string
2. number
3. boolean
4. null
5. undefined
6. symbol
7. bigint

這些都是immutable，不可改變的
> 例如: x = 3.14，只可以改變x的值，但3.14這個值不能修改

而物件的值是mutable，可改變的


## Object 
### 創建JavaScript Object
1. object literal
    - `cont obj = {}`
2. `new`
    - `const obj = new Object()`
3. object constructor
4. `Object.create()`


### Object Properties
取值方法:
1. obj.property
2. obj['property']

#### 新增屬性
直接在現有的Object給予新的property
例如:
```
const obj = {
    name: 'lauren'
}

obj.pet = 'oreo'
```

#### 刪除屬性
利用`delete`刪除特定屬性
例如:
```
const obj = {
    id: 1,
    name: 'lauren'
}

delete obj.id
console.log(obj.id) // undefined
```

### Object Methods
> a property containing a function definition
> 一個屬性，其值是function
1. 存取物件方法: objName.methodName()
2. `this`: 在物件中的function使用`this`，指向的是物件本身，但要注意
    - 箭頭函示
    - Web APIs使用
會影響到`this`的指向，更深入會在THIS章節討論



### Object資料渲染
直接將Object放到DOM，會變成**[object Object]**，必須透過property存取value

1. ObjectName.propertyName
2.  迴圈取資料

#### Object Iteration
1. Obejct.values: 傳入一個物件，直接取得所有 property value，並以陣列回傳
```
const object1 = {
  a: 'somestring',
  b: 42,
  c: false,
};

console.log(Object.values(object1));
// Expected output: Array ["somestring", 42, false]
```

> 實際應用場景: 計算總和
```
const myObj = {
    1: 100,
    2: 50,
    3: 25
}

console.log(Object.values(myObj).reduce((sum, val)=> sum += val)) //175
```

2. Object.keys(): 可以直接傳入一個物件，並將其 key 值以陣列的方式呈現。
```
const person = {
  firstName: "John",
  lastName: "Doe",
  language: "en"
};

console.log(Object.keys(person)) //['firstName', 'lastName', 'language']
```

3. Object.entries(): 將key 與 value 以陣列的方式呈現。
```
const person = {
  firstName: "John",
  lastName: "Doe",
  language: "en"
};

console.log(Object.entries(person))
```
> 結果: (3) [Array(2), Array(2), Array(2)]
    0: (2) ['firstName', 'John']
    1: (2) ['lastName', 'Doe']
    2: (2) ['language', 'en']
- 注意：排序會以key的順序為主
假如有一個Object： 
`const obj = { 10: 'adam', 200: 'billy', 35: 'chris' };`
利用Object.entries變成陣列後會成為： 
`[ [ '10', 'adam' ], [ '35', 'chris' ], [ '200', 'billy' ] ]`

## 物件中的getter與setter: Object Accessors
JavaScript中有兩種物件屬性
1. Data Properties
```
const student = {
    //data property
    firstName: 'Jane'
}
```

2. Accessor Properties
這會是一個function，使用關鍵字`get`和`set`

- get: 存取不需要加上括號
```
const student = {
    firstName: 'John',
    get getName(){
        return this.firstName
    }
}

console.log(student.firstName) //John
console.log(student.getName) //John
console.log(student.getName()) //ERROR
```

- set: 
```
const student = {
    firstName: 'Monica',
    
    //accessor property(setter)
    set changeName(newName) {
        this.firstName = newName;
    }
};

console.log(student.firstName); // Monica

// change(set) object property using a setter
student.changeName = 'Sarah';

console.log(student.firstName); // Sarah
```

### Object.defineProperty()
可以利用`defineProperty`來新增getter,setter
```
const student = {
    firstName: 'Monica'
}

// getting property
Object.defineProperty(student, "getName", {
    get : function () {
        return this.firstName;
    }
});

// setting property
Object.defineProperty(student, "changeName", {
    set : function (value) {
        this.firstName = value;
    }
});

console.log(student.firstName); // Monica

// changing the property value
student.changeName = 'Sarah';

console.log(student.firstName); // Sarah
```

reference:
https://www.programiz.com/javascript/getter-setter
https://www.w3schools.com/js/js_object_accessors.asp


TODO
1. Object.assign
2. Object constructor
3. Object prototype
JavaScript基本功修練：Day19 - 設定物件屬性裏的特徵: https://ithelp.ithome.com.tw/articles/10249020

