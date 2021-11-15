1. **null和undefined的区别**

   null指空对象，表示该处不应该有值，undefined是值未定义变量，表示该处应该有值，但是没有定义；

   null可以理解为系统级、意料之中的空缺值，而undefined是程序级、意料之外的空值；

   null转为数字是0，而undefined转为数字是NAN；

2. **ES6模板字面量**

   ```html
   <audio data-key="70" src="assets/sounds/刘德华-17岁.flac"></audio>
   ```

   ```javascript
   const audio=document.querySelector(`audio[data-key="${e.keyCode}"]`)//键盘选中的audio
   ```

   可以在${}里面引用变量

3. **数组方法**

   ```javascript
   let array = [1,2]
   arr.push(3) // [1,2,3]
   arr.unshift(0) // [0,1,2,3]
   console.log(arr.slice(0,2)) // [0,1]
   arr.pop() // [0,1,2]
   arr.shift() // [1,2]
   let arrrrrrrr = [1,2,3]
   let newArr1 = arrrrrrrr.reduce((total,value)=>total+value) // 累加器,返回值6
   let newArr2 = arrrrrrrr.filter((value)=>value>1) // 过滤，返回新数组[2,3]
   let newArr3 = arrrrrrrr.map(value=>value+1) // 遍历，返回新数组 [2,3,4]
   let newArr4 = arrrrrrrr.forEach(value=>value+1) // 遍历，不返回，或者说返回undefined
   // Array.from() 方法从一个类似数组或可迭代对象创建一个新的，浅拷贝的数组实例。
   console.log(Array.from('foo'));// expected output: Array ["f", "o", "o"]
   console.log(Array.from([1, 2, 3], x => x + x));// expected output: Array [2, 4, 6]
   ```

   会改变原数组的方法push(),pop(),unshift(),shift(),sort()默认实现是快排,reverse(),splice()

   **不**会改变原数组的方法join(),slice(),concat(),toString(),map(),forEach(),reduce(),filter()

4. **Math**数学工具对象

   Math.floor(2.6) => 2   取整

   Math.round(2.6) => 3   类似于四舍五入

   Math.ceil(2.2) => 3    向上取整

5. 类型判断

   **typeof** 判断基本类型，但是不可以判断null，反而可以判断function类型

   ```javascript
   console.log(typeof null) //object
   console.log(typeof array) // object
   console.log(typeof obj) // object
   console.log(typeof fn) // function
   ```

   **instanceof**判断引用类型

   ```javascript
   console.log(str instanceof String) //false
   console.log(num instanceof Number) //false
   console.log(null instanceof Object) //false
   console.log(obj instanceof Object) //true
   console.log(array instanceof Array) //true
   console.log(fn instanceof Function) //true
   ```

   **constructor**判断，但是判断不了没有构造器的null与undefined

   ```javascript
   console.log(str.constructor===String) //true
   console.log(array.constructor===Array) //true
   console.log(null.constructor===null) //报错
   console.log(undefined.constructor===undefined) //报错
   ```

   **对象原型的toString()**判断，较完整

   ```javascript
   console.log(Object.prototype.toString.call(str)) // [object String]
   console.log(Object.prototype.toString.call(array)) // [object Array]
   console.log(Object.prototype.toString.call(obj)) // [object Object]
   console.log(Object.prototype.toString.call(null)) // [object Null]
   console.log(Object.prototype.toString.call(undefined)) // [object Undefined]
   ```

6. 函数调用方式

   ```javascript
   // 勾股定理求斜边
   function hypotenuse(a, b) {
       function square(x){
           return x*x
       }
       return Math.sqrt(square(a)+square(b))
   }
   ```

   1. **作为函数调用**

      ```javascript
      let hptn = hypotenuse(3, 4)
      ```

   2. **作为对象方法调用**

      ```javascript
      let calculator = {
          a: 1,
          b: 2,
          add: function (){
              console.log(this) // 作为方法调用，this指向调用它的对象
              fn()
              function fn(){
                  console.log(this) // 作为函数调用，指向全局或者undefined
              }
              return this.a+this.b
          }
      }
      let result = calculator.add()
      ```

   3. **作为构造函数调用**

      ```javascript
      function Dog(name,age){
          this.name=name
          this.age=age
      }
      // es6类写法
      class Person{
          constructor(name,age) {
              this.name=name
              this.age=age
          }
      }
      let p = new Person("guo",18)
      let d = new Dog("guo",18)
      // 1. 创建一个新的空对象{}
      // 2. 将空对象的__proto__属性指向构造函数的prototype属性
      // 3. 构造函数的this指向空对象，执行构造函数
      // 4. 返回新对象
      ```

   4. **通过call(),apply()来间接调s用函数**

      ```javascript
      console.log(Object.prototype.toString.call([]))
      ```

7. **闭包**

   闭包是一种计算机特性，允许函数捕捉保存**定义**它时的局部变量。可以用来做**缓存**！！

   因为函数执行依赖于作用域链，这个作用域是在函数定义是决定的，而不是函数调用时。

   函数执行依赖于作用域链，我们可以把他理解为对象列表。

   在函数执行时，他会将**局部变量**保存为一个对象添加到作用域链中。正常情况下，在函数执行完毕后这个对象会被删除并回收，

   但是如果这个函数中定义了**嵌套函数**，这些嵌套函数也会有各自的作用域，并且**指向前面的局部变量对象**。

   这时候如果我们将嵌套函数作为**返回值**返回，用一个变量引用它，这个嵌套函数和它的作用域链就不会被回收了。

   ```javascript
   let scope = 'global'
   function checkScope(){
       let scope = 'local'
       function f() {
           return scope
       }
       return f
       // return f()
   }
   console.log(checkScope()()) // local
   //console.log(checkScope()) // local
   ```

   不管何时何地调用f()，这个scope都是'local'

8. 遍历对象的一些方式

   ```javascript
   for(let key in obj){
       // 遍历键名
   }
   for(let value of obj){
       // 遍历键值
   }
   for(let key of Object.keys(obj)){
       // 遍历键名数组
   }
   for(let value of Object.values(obj)){
       // 遍历键值数组
   }
   console.log(Object.getOwnPropertyNames({a:1})) // ['a'] 获取键名数组
   ```

10. **var let 和const**

    在非函数块声明的var变量全局可用，存在变量提升，可以重复定义

    let和const声明的变量有块级作用域，不存在变量提升，不可以重复声明

    es5语句try...catch(e)中，catch子句中的标识符e具有块级作用域

10. **箭头函数**

    **箭头函数本身不绑定 this**，this 指向的是**箭头函数所在的作用域指向的对象**

    （也就是说，箭头函数在哪个位置定义的，this 就跟这个位置的 this 指向相同）

    ```javascript
    let f = {
        fn1:function (){
            console.log(this)
        },
        fn2:()=>{
            console.log(this)
        }
    
    }
    f.fn1() // fn1普通函数this指向调用它对象,所以this指向f
    f.fn2() // fn2箭头函数，所在作用域是window(没有其他函数包裹),所以this指向window
    ```

11. **垃圾回收机制**

    JavaScript的内存管理，我的理解是，如果一个对象没有**被引用**，那么他就会不可访问，那么它就会被回收

12. **异步**

    JavaScript任务分为同步和异步，同步是指只有当前一个任务完成时才能执行下一个任务。

    这时候如果一个任务花费时间很多的话，就会造成进程堵塞，这时候就要用到异步。

    异步是指一些事件或者任务执行后立即返回，常用场景有http数据请求，定时器，Promise

13. 数组去重，set为什么不可重复原理 

    ```javascript
    let arr = [1,2,3,1]
    console.log(Array.from(new Set(arr)))
    let result= []
    for (let i of arr){
        if (result.indexOf(i)===-1){
            result.push(i)
        }
        // if (result.includes(i)){
        //     break
        // }else result.push(i)
    }
    console.log(result)
    // 两个for遍历比对，配合splice()删除重复元素
    // 利用Set集合类只能存在唯一值或引用，不可重复
    // Array.from(new Set(arr))
    // [...new Set(arr)]
    ```

14. ==和=== 

    == 判断相等，存在隐式类型转换， === 严格相等

15. 跨域解决方法（浏览器安全的限制）

    前后端交互跨域问题，后端设置通行**Access-Control-Allow-Origin**访问控制允许源

    jsonp 利用**script**标签的src属性天然跨域的特点

    ```html
    <script src="https://www.baidu.com?callback=getBaidu"></script>
    ```

    两个页面设置相同的document.domain，以共享cookie

    跨文档通信API :window.postMessage()

16. localStorage sessionStorage cookie

    localStorage 本地存储，数据永久有效，除非手动删除，作用域基于文档源（同源策略）；

    seesionStorage 会话存储，数据在窗口关闭时失效，作用域基于文档源；

    cookie 少量数据存储，一个url默认的cookie数上限20，每次cookie大小不超过4KB；

    数据有效期可以设置，默认是窗口关闭失效，

    作用域默认是文档源，可以通过cookie.domain设置

17. http

    http是指超文本传输协议（Hyper Text Transfer Protocol，HTTP）是一个请求-响应协议（它通常运行在[TCP](https://baike.baidu.com/item/TCP/33012)之上）。它指定了**客户端**可能发送给**服务器**什么样的**消息**以及得到什么样的**响应**。

18. https

    与http相比，多了基于`SSL`或者`TLS`的内容加密、身份认证和数据完整性保护

19. web语义化

    `web语义化`是指使用恰当语义的html标签、class类名等内容，让**页面**具有**良好的结构与含义**，从而让人和机器都能快速的理解网页内容。比如p标签表示段落，header标签表示页头，footer标签表示页脚等。结构清晰，有利于团队的开发和维护。

20. eventLoop

    `Javascript`是单线程的，然后它的任务分为**同步任务**和**异步任务**，

    同步任务会在**调用栈**中按照顺序等待主线程依次执行，

    异步任务会在异步任务有了结果后，将注册的回调函数放入**任务队列**中等待执行。

    具体而言，异步任务又分为宏任务（定时器）和微任务（promise），

    宏任务每次执行时检测微任务队列是否为空再执行，

    如果不为空，先执行完微任务，在执行宏任务

21. get和post区别

    get只支持url编码，post支持多种编码

    get只接收ascii字符，post没有限制

    get通过url传递参数，暴露在url上，不安全，post通过body传参

    get通过url传递的参数有长度限制，post没有

22. web攻击

    **xss**(编码 过滤)  **sql**注入  **ddos  csrf**

23. 深拷贝和浅拷贝

    深拷贝和浅拷贝是相对数组和对象来说的，浅拷贝就是遍历赋值一层对象的属性，而深拷贝是深度递归复制所有属性。

    ```javascript
    deepCopy(obj) { // 深拷贝通用方法
      if (typeof obj !== 'object' || obj === null) return obj
      let newObj = obj instanceof Array ? [] : {}
      for (let key in obj) {
        if (obj.hasOwnProperty(key)) {
          newObj[key] = typeof obj[key] === 'object' ? this.deepCopy(obj[key]) : obj[key]
        }
      }
      return newObj
    },
    ```

24. 这方面我没有经验，能不能**指点一下**？  新人培养方案  

25. 防抖和节流

    - 对于**短时间内连续触发**的事件（上面的滚动事件、鼠标移动事件），防抖的含义就是通过**闭包和定时器**让事件**停止触发**的**某个时间**后，只执行一次事件处理函数。
    - 对于**短时间内连续触发**的事件，那么在**函数执行一次之后**，该函数在**指定的时间期限内不再工作**，直至过了这段时间才重新生效。**技能冷却**

26. 原型链

    JS它是基于原型的。每个实例对象都有一个私有属性（`__proto__` /  `[[Prototype]]`）指向它的构造函数的原型对象`prototype`。该原型对象也有自己的原型对象`__proto__`,层层向上直到一个对象的原型对象为`null`

    ```javascript
    function Range(from, to) {
      this.from = from
      this.to = to
    }
    let r = new Range(1, 3)
    console.log(Object.getPrototypeOf(r) === Range.prototype) // true
    console.log(Object.getPrototypeOf(Range.prototype) === Object.prototype) // true
    console.log(Object.getPrototypeOf(Object.prototype) === null) // true
    ```

    当试图访问一个对象的属性时，它不仅仅在该对象上搜寻，还会搜寻该对象的原型，以及该对象的原型的原型，依次层层向上搜索，直到找到一个名字匹配的属性或到达原型链的末尾。**在原型链上查找属性比较耗时**。

    **继承方式**

    - 通过**构造函数**继承，在子类里绑定执行父类的构造函数（父类的原型链上的属性没有被继承）

      ```javascript
      function Parent(name, age){
          this.parentName = name
          this.parentAge = age
      }
      function Child(name, age){
          Parent.call(this.name+'s parent',age+12)
          this.childName = name
          this.childAge = age
      }
      let c = new Child('a',16)
      Parent.prototype.a = 1
      console.log(c.a) // undefined
      ```

    - 通过**原型链**继承（对于同一个构造函数的两个实例对象，他们的原型相同，改变一个实例对象，另一个对象实例也会改变）

      ```javascript
      function Parent(age){
        this.parentName = ['parentName']
        this.parentAge = age
      }
      function Child(name, age){
        //Parent.call(this.name+'s parent',age+12)
        this.childName = name
        this.childAge = age
      }
      Child.prototype = new Parent( 28)
      let c1 = new Child('child1',16)
      let c2 = new Child('child2', 16)
      console.log(c1.__proto__ === c2.__proto__) // true
      c1.parentName.push('parent of both child1 and child2')
      console.log(c1.parentName === c2.parentName) // true
      ```

27. 的

     async和defer 

     元素垂直居中 

     [算法题]()：有效括号

面试官你好，我叫郭荣华 ，毕业于中南大学的计算机专业，目前在从事和学习前端开发的工作，平时主要使用vue框架开发，然后也了解一点后台开发。