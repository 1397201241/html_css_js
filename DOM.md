1. **选取文档元素**

   ```javascript
   let byId = document.getElementById('elementId')
   let byClassName = document.getElementsByClassName('className') // HTMLCollection
   let byTagName = document.getElementsByTagName('div') // HTMLCollection
   let byName = document.getElementsByName('elementName') // nodeList
   let bySelector1 = document.querySelector('#elementId') // 第一个节点
   let bySelector2 = document.querySelectorAll('#elementId') // nodeList
   ```

2. 文档结构和遍历

   - 作为**节点树**的文档（Node节点包含Document、Element、Text、Script）

     有以下属性parentNode, childNodes, firstChild, lastChild, nextSibling, previousSibling,

     nodeType, nodeValue(Text节点的文本内容), nodeName(会转大写)

   - 作为**元素树**的文档(不包含文本节点Text)

     children, firstElementChild, lastElementChild, nextElementSibling, previousElementChild, childElmentCount子元素数量

3. **属性**

   直接获取属性

   ```javascript
   console.log(byId.parentNode.firstElementChild.id)
   ```

   **getAttribute()**获取属性

   ```javascript
   console.log(byId.parentNode.firstElementChild.getAttribute('id'))
   ```

   **attributes**获取属性

   ```javascript
   console.log(byId.parentNode.firstElementChild.attributes[0])
   ```

   setAttribute()设置属性

   ```javascript
   byId.parentNode.firstElementChild.setAttribute('id','newId')
   ```

4. 元素内容

   返回元素内容

   ```javascript
   console.log(byId.parentNode.firstElementChild.innerHTML) // das
   ```

   以字符串形式返回整个元素

   ```javascript
   console.log(byId.parentNode.firstElementChild.outerHTML) 
   // <div style="width: 10px;height: 10px;background:saddlebrown" id="elementId" data-key="key">das</div>
   ```

5. 节点操作

   创建节点

   ```javascript
   let textNode = document.createTextNode('text node') // textNode
   let element = document.createElement('p') // <p></p>
   let comment = document.createComment('text node')
   ```

   插入节点

   ```javascript
   element.appendChild(textNode) // 插入指定节点，使其成为父节点的最后一个子节点
   byId.insertBefore(element,byId.childNodes[0]) // 在父节点指定的子节点前插入一个新的子节点
   ```

   删除节点

   ```javascript
   byId.removeChild(byId.childNodes[0]) // 删除子节点
   byId.replaceChild(document.createTextNode("sad"),byId.childNodes[0]) // 删除子节点，并替换为新节点
   ```

6. 冒泡与捕获

   DOM事件流有两种，捕获和冒泡

   捕获就是从最外层元素（window）向下捕获直到目标元素

   冒泡就是从目标元素向上冒泡直到最外层元素，chrome默认是冒泡

7. **事件委托**

   事件委托，通俗地来讲，就是把一个元素（click、keydown......）的事件处理函数委托到另一个元素。一般是利用**冒泡**事件流，为父元素注册监听器，子元素触发事件后会向上冒泡给父元素，父元素通过`event.target`获取触发事件的元素并进行相应的处理。

   ```html
   <ul>
       <li>a</li>
       <li>b</li>
       <li>c</li>
   </ul>
   ```
   
   ```javascript
   let ul = document.getElementsByTagName('ul')[0]
   ul.addEventListener('click',(e)=>{
       if (e.target&&e.target.nodeName === 'LI'){
          alert(e.target.innerHTML)
       }
   }, false)
   ```
8. 性能优化

   - 资源压缩合并，减少http请求

   - 异步加载非核心脚本（**defer**按照加载的顺序依次执行脚本, **async**加载完立即执行）

   - 利用浏览器缓存,下次请求时，可以直接从本地读取，不用重新请求资源

     利用http响应头的expires或者Cache-Control实现

9. ### 遇到不知道的问题，该怎么回答

   - 这块儿我没了解过，准备回去看一下。
   - 这块儿我没研究过，您有没有好的资料，我可以补充一下细节。
   - 写不出详细的代码，但是知道思路。

10. **垃圾回收机制**

    JavaScript的内存管理，我的理解是，如果一个对象没有**被引用**，那么他就会不可访问，那么它就会被回收

11. **异步**

    JavaScript任务分为同步和异步，同步是指只有当前一个任务完成时才能执行下一个任务。

    这时候如果一个任务花费时间很多的话，就会造成进程堵塞，这时候就要用到异步。

    异步是指一些事件或者任务执行后立即返回，常用场景有http数据请求，定时器，Promise

12. 数组去重，set为什么不可重复原理 

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

13. ==和=== 

    == 判断相等，存在隐式类型转换， === 严格相等

14. 跨域解决方法

    前后端交互跨域问题，后端设置通行**Access-Control-Allow-Origin**访问控制允许源

    jsonp 利用**script**标签的src属性天然跨域的特点

    ```html
    <script src="https://www.baidu.com?callback=getBaidu"></script>
    ```

    两个页面设置相同的document.domain，以共享cookie

    跨文档通信API :window.postMessage()

15. localStorage sessionStorage cookie

    localStorage 本地存储，数据永久有效，除非手动删除，作用域基于文档源（同源策略）；

    seesionStorage 会话存储，数据在窗口关闭时失效，作用域基于文档源；

    cookie 少量数据存储，一个url默认的cookie数上限20，每次cookie大小不超过4KB；

    数据有效期可以设置，默认是窗口关闭失效，

    作用域默认是文档源，可以通过cookie.domain设置

16. https 

    与http相比，多了基于ssl或者tls的内容加密、身份认证和数据完整性保护

17. 用css画个三角形 

    ```css
    .triangle{
        height:0;
        width:0;
        border-bottom: 10px solid red;
        border-left: 10px solid transparent;
        border-right: 10px solid transparent
    }
    ```

18. Vue双向数据绑定大致原理

    ```javascript
    let span = document.getElementsByTagName('span')[0]
    let dom = document.getElementById('dom')
    let obj={}
    Object.defineProperty(obj,'val',{
        get:function () {
            return this.val
        },
        set(v) {
            this.val=v
            dom.innerHTML=v
            span.innerHTML=v
        }
    })
    dom.addEventListener('keyup',e=>{
        obj.val = e.target.value
    })
    ```

19. Vue-Router的两种模式

    **hash**模式   #后面 hash 值的变化，并**不会导致浏览器向服务器发出请求**，浏览器不发出请求，也就不会刷新页面。

    **history**模式  利用HTML5 History api新方法pushState()和replaceState()修改url且不会发送请求，

    可以**修改**浏览器历史记录栈，但是需要后台配置

20. get和post区别

    get只支持url编码，post支持多种编码

    get只接收ascii字符，post没有限制

    get通过url传递参数，暴露在url上，不安全，post通过body传参

    get通过url传递的参数有长度限制，post没有

21. web攻击

    **xss**(编码 过滤)  **sql**注入  **ddos  csrf**

22. 三栏布局

    float  绝对定位 flex布局  grid布局  table布局

    flex=1自动分配           grid-template-columns:100px auto 100px

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

24. css动画

    关键帧@keyframs + animation

    定时器红宝书 mdn  codewars

25. v-if通过dom操作元素的添加和删除来控制元素的显隐

    v-show通过改变元素的 css 属性（display）来决定元素的显隐

26. 这方面我没有经验，能不能**指点一下**？  新人培养方案  

27. 

    

     async和defer 

     元素垂直居中 

     vue-router的两种模式以及区别 

     vue响应式原理 

     [算法题]()：有效括号

