---
title: 前端开发面试题--CSS(一)
date: 2018-11-5 13:57:35
tags:
  - CSS
  - 面试题
  - 前端
categories: 
  - 面试题
  - CSS
---

> 以下内容来自：https://segmentfault.com/a/1190000013325778

### 介绍CSS盒模型, 与低版本IE的盒模型有何不同?
```bash
标准盒子模型：
  宽度 = 内容长度(content) + border + padding + margin12
低版本IE盒子模型：
  宽度 = 内容长度(content + border + padding) + margin
```

### box-sizing 属性?
```bash
用来控制盒子模型的解析模式, 默认为 content-box

content-box：W3C的标准盒模型
   设置元素的 height/width 属性只包含 content 部分的高/宽
   
border-box：IE传统盒模型
   设置元素的 height/width 属性包含 border + padding + content 部分的高/宽  
```

### CSS选择器有哪些? 哪些是可以继承的?
```bash
CSS选择器：
  #eleid
  .className 
  element
  ele + ele
  ele > ele 
  ele ele 
  *
  ele[rel="value"]
  ele:hover
  ele:nth-child
  
可继承的属性：
  font-size  font-family  color
  
不可继承的样式：
  border  padding  margin  width  height
    
优先级(就近原则)：!important > [id > class > tag]
  !important 比内联优先级高
```

### CSS优先级算法如何计算?
```bash 
元素选择符：1
class选择符：10
id选择符：100
元素标签：1000
  
  !important 声明的样式优先级最高, 如果冲突在进行计算
  优先级相同则选择最后出现的样式
  继承得到的样式优先级最低
```

### CSS3新增的伪类?
```bash
ele:first-of-type 
ele:last-of-type
ele:only-of-type
ele:only-child
ele:nth-child(n)
:enabled :disabled 
:checked 
```

### 如何居中一个div
```bash
div:
    border: 1px solid red;
    margin: 0 auto;
    height: 50px;
    width: 80px;
    
浮动元素的上下左右居中：
  border: 1px solid red;
  float: left;
  position: absolute;
  width: 200px; 
  height: 100px;
  left: 50%;
  top: 50%;
  margin: -50px 0 0 -100px;
  
绝对定位的左右居中：
  border: 1px solid black;
  position: absolute;
  width: 200px; 
  height: 100px;
  margin: 0 auto;
  left: 0;
  right: 0;
```

### display有哪些值?  
```bash
inline(默认) -- 内联
none -- 隐藏
block -- 块显示
table -- 表格显示
list-item -- 项目列表 ??
inline-block -- 行内块显示
```

### position的值?
```bash
static(默认)：按照正常文档流进行排列;
relative(相对定位)：不脱离文档流, 参考自身静态位置通过 top  bottom  left  right 定位;
absolute(绝对定位)：参考距其最近的一个 不是static 的父元素通过 top  bottom  left  right 定位;
fixed(固定定位)：所固定的参照对象是可是窗口;
```

### CSS3有哪些新特性? 
```bash
1. 颜色：
      rgba 和透明度

2. 阴影：
     text-shadow: 文字阴影 
     box-shadow: 盒阴影
        text-shadow: 5px 5px 5px #f00; (水平阴影, 垂直阴影, 模糊距离, 阴影颜色)
    
3. 背景相关：
     background-image
     background-origin(content-box/padding-box/border-box)
     background-size
     background-repeat

4. 边框：
     border-radius 属性：边框半径(圆角)
     border-image 属性：边框图片
       border-image: url(border.png) 30 30 round
       
5. 字体：
     font-face属性：定义自己的字体

6. 换行：
     word-wrap  
        word-wrap: break-word
        
7. 媒体查询：定义两套CSS, 当浏览器地尺寸变化时回采用不同的属性
```

### 解释 CSS3 的 flexbox(弹性和布局模型), 以及使用场景? 
```bash
该布局模型的目的是提供一种更加高效的方式来对容器的条目进行布局, 对齐和分配空间
传统布局方式中, block 布局是把块在垂直方向从上到下依次排列; inline 布局则是在水平方向来布局
弹性盒布局并没有这样内在的方向限制, 可以由开发人员自由操作

适用场景：移动前端开发
```

### 用 纯CSS 创建一个三角形的原理是什么? 
```bash
首先把元素的宽度, 高度设为0, 然后设置边框样式
  width: 0; height: 0;
  border-top: 40px solid transparent;
  border-right: 40px solid transparent;
  border-bottom: 40px solid transparent;
  border-left: 40px solid #f00;
```

### 一个满屏'品'字布局如何设计?
```bash
a. 真正的品字
  1. 三块高度是确定的;
  2. 上面那块用 margin： 0 auto; 实现居中
  3. 下面两块用 float 或 inline-block 不换行
  4. 用 margin 调整位置使他们居中

b. 全屏品字布局
  上面的 div 设置成 100%; 
  下面的 div 分别宽 50%, 然后使用 float 或者 inline 使其不换行
```

### 常见的兼容问题? 
```bash
1. 不同浏览器的标签默认的 margin 和 padding 不一样
    *{margin: 0; padding: 0}
2. IE6 双边距bug 块属性标签 float 后, 又有横行的margin情况下, 在IE6显示 margin 比设置的大
    hack： display: inline; 将其转化为行内属性
3. 渐进识别的方式, 从总体中逐渐排除局部. 
    首先, 巧妙的使用 '9' 这一标记, 将IE浏览器从所有情况中分离出来
    接着, 再次使用 '+' 将IE8和IE7、IE6分离出来, 这样IE8已经独立识别
      {
        background-color: #f1ee18; /* 所有识别 */
        .background-color: #00deff\9; /* IE6、7、8识别 */
        +background-color: #a200ff; /* IE6、7识别 */
        _background-color: #1e0bd1; /* IE6识别 */
      }
4. 设置较小高度标签(一般小于10px), 在IE6, IE7中高度超出自己设置高度
     hack： 给超出高度的标签设置 overflow: hidden; 
            或者设置行高line-height 小于你设置的高度
5. IE下, 可以使用获取常规属性的方法来过去自定义属性, 也可以使用 getAttribute() 获取自定义属性
   Firefox下, 只能使用 getAttribute() 获取自定义属性
     解决：统一使用 getAttribute() 获取自定义属性
6. Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示
     解决：加入CSS属性 -webkit-text-size-adjust: none;
7. 超链接访问过后 hover 样式就不出现了, 被惦记访问过的超链接样式不再具有 hover 和 active
     解决：改变CSS属性的排列顺序：L-V-H-A(love hate) a:link{} a:visited{} a:hover{} a:active{}
```

### 为什么要初始化CSS样式
```bash
因为浏览器兼容问题, 不同浏览器对有些标签的默认值是不同的, 如果没对CSS初始化会出现浏览器之间的页面显示差异
```

### absolute 的 containing bock 计算方式和正常流有何不同? 
```bash
无论哪种, 都要先找到其祖先元素中最近的 position 值 不为static 的元素, 然后在判断
  1. 若此元素为 inline 元素, 则 containing block 为能够包含这个元素的第一个和
     最后一个inline box 的padding box(除 margin, border 外的区域)的最小矩形
  2. 否则, 则由这个祖元素的padding box 构成
  
 如果都找不到, 则为 initial containg box
 
 另：
    1. static/relative: 简单来说就是他父元素的内容框(即去掉padding的部分)
    2. absolute: 向上找最近的定位为 absolute/relative 的元素
    3. fixed: 它的containing block 一律为根元素(html/body)
```

### CSS里的 visibility 属性有个 collapse 属性值, 在不同浏览器下有什么区别?
```bash
当一个元素的 visibility属性被设置成 collapse 值后, 对于一般的元素, 它的表现跟hidden是一样的
  1. Chrome中, 使用 collapse 值和使用 hidden 没区别
  2. Firefox, opera 和IE, 使用 collapse 值和使用 display: none 没有区别
```

### display: none 和 display: hidden 的区别?
```bash
display: none; 不显示对应的元素, 在文档布局中不再分配空间(回流 + 重绘)
display: hidden; 隐藏对应元素, 在文档布局中仍保留原来的空间 (重绘)
```

### position 跟 display、overflow、float这些特性相互叠加后悔怎样?
```bash
display 属性规定元素应该生成的框的类型; 
position 属性规定元素的定位类型; 
float 属性是一种布局方式, 定义元素在哪个方向浮动;
类似于优先级机制：position: absolute/fixed 优先级最高, 有他们在时, float不起作用,
display 值需要调整; float或absolute定位的元素, 只能是块元素或表格
```

### 对 BFC(块级格式化上下文：block formatting context)规范的理解?
```bash
BFC 规定了内部的 Block Box 如何布局
定位方案：
    1. 内部的 Box 会在垂直方向上一个接一个放置
    2. Box 垂直方向的距离由 margin 决定, 属于同一个 BFC 的两个相邻 Box 的margin 会发生重叠
    3. 每个元素的 margin box 的左边, 与包含块 border box 的左边相接触
    4. BFC 的区域不会与 float box 重叠
    5. BFC 是页面上的一个隔离的独立容器, 容器里面的子元素不会影响到外面的元素
    6. 计算 BFC 的高度是, 浮动元素也会参与计算
 
 满足以下条件之一即可触发 BFC：
    a. 根元素, 即 html
    b. float 的值不为 none(默认)
    c. overflow 的值不为 visible(默认)
    d. display 的值为 inline-block, table-cell, table-caption
    e. position 的值为 absolute 或 fixed
```

### 为什么会出现浮动和什么时候需要清除浮动, 清除浮动的方式?
```bash
浮动元素碰到包含它的边框后者浮动元素的边框停留, 由于浮动元素不再文档流中, 
所以文档流的块框表现的就像浮动框不存在一样, 浮动元素会漂浮在文档流的块框上

浮动带来的问题：
  1. 父元素的高度无法被撑开, 影响与父元素同级的元素
  2. 与浮动元素同级的非浮动元素(内联元素)会跟随其后
  3. 若非第一个元素浮动, 则该元素之前的元素也需要浮动, 否则会影响页面显示的结构

清除浮动的方式
  1. 父级 div 定义 height
  2. 最后一个浮动元素后加空 div 标签, 并添加样式 clear: both
  3. 父元素用伪类 :after ,设置context: ''; display: block; clear: both;
  4. 父级 div 定义 zoom
```

### 上下 margin 重合的问题
```bash
在重合元素外包裹一层容器, 并触发该容器生成一个BFC

ex:
  html:
    <div class="aside"></div>
    <div class="text">
        <div class="main"></div>
    </div>
  css: 
    .aside{
      margin-bottom: 100px;
      width: 100px; height: 150px;
      background: #666;
    }
    .main{
      margin-top: 100px;
      height: 200px;
      background: #fcc;
    }
    .text{
      /* 盒子 main 的外面包一个 div, 通过改变此 div 的属性是两个盒子分属与两个不同的 BFC */
      overflow: hidden; // 此时已经触发了 BFC 
    }
```

### 设置元素浮动后, 该元素的 display 值?
```bash
自动变为display: block
```

### 媒体查询?
```bash
通过媒体查询可以为不同大小和尺寸的媒体定义不同的css, 适应相应的设备显示
1. <head>里边
  <link rel='stylesheet' type='text/css' href='xxx.css' media='only scren and (max-device-width: 480px)'>
2. CSS: @media only screen and (max-device-width: 480px){ /CSS样式/ }
```

### CSS预处理器?
```bash
Less Sass
```

### CSS优化, 提高性能的方法有哪些?
```bash
1. 避免过度约束
2. 避免后代选择器
3. 避免链式选择符
4. 使用紧凑的语法
5. 避免不必要的重复
6. 避免不必要的命名空间
7. 最好使用表示语义的名字
8. 避免 !important, 可选择其他选择器
9. 尽可能的精简规则, 合并不同类里的重复规则
```

### 浏览器是怎样解析CSS选择器的?
```bash
CSS选择器的解析是从右到左解析, 若从左向右的匹配, 发现不符合规则, 需要进行回溯, 会损失很多性能;
若从右向左匹配, 先找到所有的最右节点, 对于每一个节点, 向上寻找其父节点直到找到根元素或满足条件的匹配规则,
则结束这个分支的遍历,两种匹配规则的性能差别很大, 是因为从右向左的匹配规则在第一步就筛选掉了大量的不符合条件的最右节点,
而从左向右的匹配规则的性能都浪费在了失败的查找上面
在CSS解析完毕后, 需要将解析的结果与DOM Tree的内容一起进行分析建立一棵Render Tree, 最终用来进行绘图,
在建立Render Tree 时, 浏览器就要为每个DOM Tree 中的元素根据CSS的解析结果(Style Rules)来确定生成怎样的RenderTree
```

### 在网页中应该使用奇数还是偶数的字体? why?
```bash
使用偶数字体. 
偶数字号相对更容易和 web 设计的其他部分构成比例关系.
Windows 自带的点阵宋体（中易宋体）从 Vista 开始只提供 12、14、16 px 这三个大小的点阵，
而 13、15、17 px时用的是小一号的点。（即每个字占的空间大了 1 px，但点阵没变），于是略显稀疏
```

### margin 和 padding 分别适合什么场景使用?
```bash
何时使用margin：
  1. 需要在 border 外侧添加空白
  2. 空白处不需要背景色
  3. 上下相连的两个盒子之间的空白, 需要相互抵消时

何时使用padding：
  1. 需要在 border 内侧添加空白
  2. 空白处需要背景颜色
  3. 上下相连的两个盒子的空白, 希望为两者之和
```

### 元素竖向的百分比设定是相对于容器的高度吗?
```bash
按百分比设定一个元素的宽度或者其他表示竖向距离的属性padding-top, padding-bottom, margin-top, margin-bottom等
都是相对于父容器的宽度计算的
```

### 全屏滚动的原理是什么? 用到了 CSS 的哪些属性?
```bash
1. 原理：类似轮播, 整体的元素一直排列下去, 假设有5个需要展示的全屏也米娜, 那么高度是500%, 只是展示100%; 
  剩下的可以通过 transform 进行y轴定位, 也可以通过 margin-top 实现
2. overflow: hidden; transition: all 1000ms ease;
```

### 响应式设计的基本原理, 如何兼容低版本IE?
```bash
响应式网站设计是一个网站能够兼容多个终端, 而不是为每一个终端做一个特定的版本
基本原理是通过媒体查询检测不同的设备屏幕尺寸做处理
页面头部必须有 meta 声明的 viewport
<meta name='viewport' content='width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no'>
```

### 视差滚动效果?
```bash
视差滚动(Parallax Scrolling)通过在网页向下滚动的时候, 控制背景的移动速度比前景的移动速度慢来创建出令人惊叹的3D效果
1. CSS3实现
    优点：开发时间短, 性能和开发效率比较好, 缺点是不能兼容到低版本的浏览器
2. jQuery实现
    通过控制不同层滚动速度, 计算每一层的时间, 控制滚动效果
    优点：能兼容到各个版本, 效果可控性好
    缺点：开发起来对制作者要求高
3. 插件实现方式
    例如：parallax-scrolling, 兼容性十分好
```

### ::before he :after 中双冒号和但冒号有什么区别? 这两个伪元素的作用?
```bash
1. 单冒号用于CSS3伪类, 双冒号用于CSS3伪元素
2. ::before 就是以一个子元素的存在, 定义在元素主体内容之前的一个伪元素, 并不纯在与 DOM 之中只存在页面之中
:before 和 :after 这两个伪元素, 是在CSS2.1里出现的, 伪元素前缀使用单冒号, CSS3的规范里, 伪元素语法被修改成使用双冒号
```

### 对line-height是如何理解的?
```bash
行高时指一行文字的高度, 具体是说两行文字基线的距离, CSS中起高度作用的是 height 和 line-height, 
没有定义 height 属性, 最终其表现作用一定是line-height
单行文本垂直居中：把 line-height 值设置为 height 一样大小的值可以实现单行文字的垂直居中
多行文本垂直居中：需要设置 display 属性为 inline-block
```

### 怎样让Chrome支持小于12px的文字
```bash
p{font-size: 10px; -webkit-transform: scale(.8);} // .8是缩放比例
```

### 让页面里的字体变清晰, 变细用CSS怎么做?
```bash
-webkit-font-smoothing在window系统下没有起作用, 但是在IOS设备上起作用
-webkit-font-smoothing: antilliased 是最佳的, 灰度平滑
```

### position: fixed; 在 Android 下无效怎么处理
```bash
<meta nam="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no">
```

### 如果需要手动写动画, 你认为最小时间间隔是多久, 为什么?
```bash
多数显示器默认频率是60Hz, 即1秒刷新60次, 所以理论上最小间隔为 1/60 * 1000ms = 16.7 ms
```

### li 与 li 之间有看不见的空白间隔是什么原因引起的? 如何解决?
```bash
行框的排列会受到中间空白(回车空格)等的影响, 因为空格也属于字符, 这些空白也会被应用样式, 占据空间, 所以会有间隔,
把字符大小设为0, 就没有空格了
解决：
    1. 可以将 <li> 代码全都写在一排
    2. 浮动 li 中 float: left
    3. 在 ul 中用 font-size: 0; (谷歌不支持); 可以使用letter-space: -3px;
```

### display: inline-block 时候会显示间隙?
```bash
1. 有空格的时候会有间隙, 解决：移除空格
2. margin 正值的时候, 解决：margin使用负值
3. 使用 font-size 时候, 解决：font-size: 0, letter-spacing, word-spacing
```

### 有一个高度自适应的 div, 里面有两个 div, 一个高度100px, 希望另一个填满剩下的高度
```bash
外层 div 使用position: reltive; 
高度要求自适应的 div 使用position: absolute; top: 100px; bottom: 0; left: 0;
```

### png, jpg, gif 这些图片格式解释一下, 分别什么时候用, 有没有了解过 webp?
```bash
1. png 是便携式网络图片, 是一种无损数据压缩位图文件格式, 优点是： 压缩比高, 色彩好
2. jpg 是一种针对相片使用的一种失真压缩方法, 是一种破坏性的压缩, 在色调及颜色拼花变化做的不错, 在www上被用来存储和传输照片的格式
3. gif 是一种位图文件格式, 以8位色重现真色彩的图像, 可以实现动画效果
4. webp 格式是谷歌在2010年推出的图片格式, 压缩率只有jpg的2/3, 大小比png小了45%; 缺点是压缩的时间更久, 兼容性不好, 目前谷歌和opera支持
```

### style标签写在body后与body前有什么区别?
```bash
页面加载自上而下, 当然是先加载样式
写在body标签后由于浏览器以逐行方式对HTML文档进行解析, 当解析到写在尾部的样式表会导致浏览器停止之前的渲染, 等加载且解析样式表完成之后重新渲染, 
在window的IE下可能会出现页面闪烁问题
```

### CSS属性overflow属性定义溢出元素内容区的内容会如何处理?
```bash
scroll 出现滚动条
auto 子元素内容大于父元素时出现滚动条
visible 溢出的内容出现在父元素之外
hidden 溢出隐藏
```

### CSS Sprite?
```bash
将一个页面涉及到不轻易改的图片包含到一张大图中去, 然后利用CSS的background-image, background-repeat, background-position的组合进行背景定位
利用CSS Sprites 能很好地减少网页的HTTP请求, 从而大大的提高页面的性能; CSS Sprites能减少图片的字节
```
