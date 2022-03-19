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
   <!DOCTYPE html>
   <html lang="en">
   <head>
       <meta charset="UTF-8">
       <title>Vue2双向绑定</title>
   </head>
   <body>
   <input id="input"></input>
   <span id="span"></span>
   </body>
   <script>
     let obj = {}
     let input = document.getElementById('input')
     let span = document.getElementById('span')
     // 数据劫持
     Object.defineProperty(obj, 'text', {
       configurable: true,
       enumerable: true,
       set(newVal) {
         input.value = newVal
         span.innerText = newVal
       }
     })
     // 输入监听
     input.addEventListener('keyup', function (e) {
       obj.text = e.target.value
     })
   </script>
   </html>
   ```

   vue2利用`Object.defineProperty()`的存取器，在修改数据的同时更新视图

   vue3利用ES6的`Proxy`对象实现，相对于前面的方法它还可以修改数组

5. v-for列表渲染，要绑定key值

   该指令可以基于数据源重复地渲染元素

   ```vue
   <div v-for="(item,index) of items" class="key" :data-key="item.dataKey" :key="item.id">
     <kbd>{{ item.kbd }}</kbd>
     <span class="sound">{{item.description}}</span>
   </div>
   ```

   为了给 Vue 一个提示，以便它能**跟踪**每个节点的身份，从而**重用和重新排序**现有元素，你需要为每项提供一个**唯一** `key`

6. vuex和什么时候要用**vuex**

7. vue中的data通过匿名函数返回一个对象，主要是给每个组件（比如复用型组件）声明一个私有数据空间，防止全局污染

8. data中的数据绑定，data中的对象或者数据的直接修改不会触发数据绑定，所以也不会更新视图，可以直接给this.list = ['修改后的数组']，触发视图更新

9. props对象和数组的默认值

   ```vue
   list: {
     type: Array,
     default: _ => []
   },
   obj: {
     type: Object,
     default: _ => {}
   }
   ```

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

    

18. css动画

    关键帧@keyframs + animation

    定时器红宝书 mdn  codewars

19. transform变换后不脱离标准流，原来的位置还占据着；

21. 记录一件蠢事，在表单中，下面的代码会产生意向不到的笑话

    ```javascript
    this.form.creator = this.form.user // 双向绑定了，为什么能写出这个代码啊 ?guorh?
    ```

26. 发



