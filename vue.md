1. MVVM

   MVVM模型包含View视图层、Model数据层和ViewModel控制层，通过ViewModel实现View层和Model层的双向绑定，View的变化会自动更新到ViewModel，ViewModel的变化也会自动同步到View

2. 数据绑定

   数据绑定就是将数据和视图关联，当数据变化时，可以自动更新视图。

   一个是通过`{{}}`文本插值的形式，还有就是通过`v-前缀`的指令绑定

3. v-if和v-show的区别

   v-if通过dom操作元素的添加和删除来控制元素的显隐

   v-show通过简单地切换元素的 css 属性（display）来控制元素的显隐

   v-if切换消耗更高，v-show初始化渲染消耗更高

   v-if适用于运行时条件不怎么改变的场景，v-show适用于频繁切换

4. Vue双向数据绑定大致原理， vue 2、vue3 双向数据绑定的实现、使用区别。

   `v-model` 本质是监听用户的输入事件以更新数据，并对一些极端场景进行一些特殊处理。

   `v-model`后面还可以接参数，number将输入自动转化为数字，lazy，deboundce防抖

   ```javascript
   let span = document.getElementsByTagName('span')[0]
   let input = document.getElementById('input')
   let obj={}
   Object.defineProperty(obj,'val',{
       get:function () {
           return this.val
       },
       set(v) {
           input.value=v
           span.innerHTML=v
       }
   })
   dom.addEventListener('keyup',e=>{
       obj.val = e.target.value
   })
   ```

   vue2利用`Object.defineProperty()`的存取器，在修改数据的同时更新视图

   vue3利用ES6的`Proxy`对象实现，相对于前面的方法它还可以修改数组

5. v-for列表渲染

   该指令可以基于数据源重复地渲染元素

   ```vue
   <div v-for="(item,index) of items" class="key" :data-key="item.dataKey" :key="item.id">
     <kbd>{{ item.kbd }}</kbd>
     <span class="sound">{{item.description}}</span>
   </div>
   ```

   为了给 Vue 一个提示，以便它能**跟踪**每个节点的身份，从而**重用和重新排序**现有元素，你需要为每项提供一个**唯一** `key`

6. vuex和什么时候要用**vuex**

7. s

8. 是

9. 是

10. vuex和什么时候要用**vuex**

    Vuex 是 Vue.js 的**状态管理模式**。它采用集中式存储管理所有组件的状态，

    包含state, getter, mutation, action四个部分

    它可以帮助我们管理共享状态，一种情况是跨组件共享数据，

    另一种情况是一个组件需要多次派发事件（我们就可以用mutation来统一管理）

11. vue-router的两种模式以及区别 

    **hash**模式   利用`window.hashchange`监听 hash 值的变化，加载不同的组件。它**不会导致浏览器向服务器发出请求**，浏览器不发出请求，也就不会刷新页面。

    ```javascript
    window.onhashchange = function(event){
      console.log(event.oldURL, event.newURL);
    }
    ```

    **history**模式  利用HTML5 **History** api新方法pushState()和replaceState()完成url跳转且不会重新加载页面

    ```javascript
    window.history.pushState(stateObject, title, URL)
    window.history.replaceState(stateObject, title, URL)
    ```

    可以**修改**浏览器历史记录栈，但是需要后台配置

12. 

13. 

14. 浮动

    浮动的元素会脱离标准流，导致高度塌陷问题，可能会影响后边布局

    清除浮动的方法是包含浮动contain float

    给**包含浮动的元素**添加clear类、空标签

    ```css
    .clearfix::after{
      display: block;
      content: '';
      clear: both;
    }
    ```

15. flexbox弹性容器布局

    flex=1包含三个属性，如下

    ```css
    flex: 1;
    flex-grow: 1;
    flex-shrink: 1;
    flex-basis: 0;
    ```

    分别代表放大  缩小 和 元素基准值   

    可以均匀分配弹性容器剩余宽度

16. 用css画个三角形 

    ```css
    .triangle{
        height:0;
        width:0;
        border-bottom: 10px solid red;s
        border-left: 10px solid transparent;
        border-right: 10px solid transparent;
        border-top: 10px solid transparent
    }
    ```

17. 三栏布局

    float  绝对定位 flex布局  grid布局  table布局

    flex=1自动分配           grid-template-columns:100px auto 100px

18. css动画

    关键帧@keyframs + animation

    定时器红宝书 mdn  codewars

19. transform变换后不脱离标准流，原来的位置还占据着；

20. position定位

    static默认定位，按照文档流定位，left, top等属性无效

    absolute绝对定位，相对于最近的祖先定位元素（默认是html根元素），元素脱离文档流

    fixed固定定位，相对于浏览器视口定位，元素脱离文档流，原来的位置会被占据

    relative相对定位，相对于原来的位置定位，不会脱离文档流，原来的位置不会被占据

21. 

    

22. 渐变

23. 阴影

24. 过渡

25. 变换

    

26. 发









 async和defer 

 元素垂直居中 

 

 vue响应式原理 

 [算法题]()：有效括号
