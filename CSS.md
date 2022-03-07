1. **层叠+优先级+源码顺序**

   样式来源：作者样式表（你定义的CSS）> 默认样式表

   优先级：!important(提升优先级) > 行内样式 > id选择器 > class选择器 > 标签选择器

   伪类选择器比如:hover优先级跟类选择器相同，通用选择器（*）和>、+、~对优先级无影响

   声明顺序：优先级相同时，后边出现的声明会覆盖前面的声明

   关键字：inherit继承于父元素，initial初始化为默认值

2. **相对单位**

   1em = 当前元素的字号大小

   1rem = 根元素<html>的字号大小（默认是16px）

   1vw = 网页可见部分宽度度的1/100，包含滚动条

   1vh = 网页可见部分高度的1/100

3. calc()定义字号

   ```css
   :root {
       font-size:calc(1em + 1vw)
   }
   ```

4. **自定义css属性**(必须要声明块里)

   ```css
   :root{
     --min-height: 10px;
   }
   ```

5. 盒子模型

   ```css
   box-sizing:content-box;/*标准盒模型边框盒模型width = width of content*/
   box-sizing:border-box; /*边框盒模型width = border+padding+width of content*/
   ```

   开发时，建议全局所有元素和伪类元素设置为border-box

6. 浮动

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

7. flexbox弹性容器布局

   flex=1包含三个属性，如下

   ```css
   flex: 1;
   flex-grow: 1;
   flex-shrink: 1;
   flex-basis: 0;
   ```

   分别代表放大  缩小 和 元素基准值   

   可以均匀分配弹性容器剩余宽度

8. 用css画个三角形 

   ```css
   .triangle{
       height:0;
       width:0;
       border-bottom: 10px solid red;
       border-left: 10px solid transparent;
       border-right: 10px solid transparent;
       border-top: 10px solid transparent
   }
   ```

24. 三栏布局

    float  绝对定位 flex布局  grid布局  table布局

    flex=1自动分配           grid-template-columns:100px auto 100px

27. css动画

    关键帧@keyframs + animation

    定时器红宝书 mdn  codewars

28. transform变换后不脱离标准流，原来的位置还占据着；

12. position定位

    static默认定位，按照文档流定位，left, top等属性无效

    absolute绝对定位，相对于最近的祖先定位元素（默认是html根元素），元素脱离文档流

    fixed固定定位，相对于浏览器视口定位，元素脱离文档流，原来的位置会被占据

    relative相对定位，相对于原来的位置定位，不会脱离文档流，原来的位置不会被占据

13. 媒体查询使用media规则选择满足条件的设备

    ```css
    @media (min-width: 560px) {
      .title>h1{
        font-size: 2.25rem;
      }
    }
    ```

14. 渐变

15. 阴影

    ```css
    box-shadow: #bbd0d5 100px 100px 200px 200px inset;
    ```

16. 过渡

17. 变换

18. 动画

    @keyframes规则 + **animation**

    ```css
    @keyframes moveLeftIn {
      0%{
        background: #38a725;
        transform: translate3d(0,0,0);
      }
      50%{
        transform: translate3d(100px,0,100px);
        background: #237bdc;
      }
      100%{
        background: #38a725;
        transform: translate3d(0,0,0);
      }
    }
    .animation{
    	animation: moveLeftIn 1.5s ease-in-out infinite;
    }
    ```

19. 单行字体溢出省略

    ```css
    .text-overflow {
      overflow: hidden;
      text-overflow: ellipsis;
      white-space: nowrap;
    }
    ```

20. 多行文字溢出省略

    ```css
    .textArea-overflow {
      overflow: hidden;
      text-overflow: ellipsis;
      display: -webkit-flex;
      -webkit-line-clamp:2;
      -webkit-box-orient: vertical;
    }
    ```
    
21. 元素事件失效属性

    ```css
    .disable-event {
      pointer-events: none;// 使元素上的事件失效，可配合地图，加阴影透明效果
    }
    ```

22. 背景图通过padding实现宽高自适应

    ```css
    .good-background {
      width: 100%;
      position: relative;
      padding-bottom: 5.89151%;// 图片的高比宽
      background: url("background.png") no-repeat center top;
      background-size: 100% auto;
    }
    ```

23. 默认情况下，元素的宽为100%，但是对于高度来说，如果元素的父元素高度没有设定时，该元素的高度也没0

24. 





