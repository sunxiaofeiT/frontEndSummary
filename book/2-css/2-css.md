# 前端面试总结 - CSS

## 一、CSS选择器

- 通配符选择器（*）
- 类选择器
- ID选择器
- 属性选择器（*[name]）
- 后代选择器(.classname .otherclassname)
- 子元素选择器（h1>strong)
- 相邻兄弟选择器(.classname + .classname)
- 伪类（button:active, p:first-child, q:lang(no),focus,hover,link,vistied,)
- 伪元素（first-line, first-letter, :before, :after,)

> 1.后代选择器和子元素选择器的区别是，后代选择器的两个元素的层次间隔可以是任意的，而子元素选择器只能选择前边元素的子元素。  
> 2.相邻兄弟选择器，选择的是后边的元素。

## 二、CSS属性

### 1. transform

旋转：transform：rotate(7deg);

> css中的相关度数：① deg：度数，总共360度; ② grad：梯度，一个圆400梯度； ③ rad：弧度，Π； ④ turn：圈，几圈。

### 3. Position

- static: 
    默认值，没有定位，元素出现在正常流中，（忽略top、bottom、left、right、z-index）
- relative: 
    生成相对定位的元素，可以通过top、bottom、left、right相对于正常位置进行定位，可以通过z-index分层。正常流中仍然有relative的位置，只是进行了偏移。定位总是相对于最近的父元素，无论其是何种定位方式。
- absolute: 
    生成绝对定位的元素，相对于static定位外的第一个元素进行定位，元素的位置通过"left","top","right"以及"bottom"属性进行规定。可通过z-index进行层次分级。正常流中不再有absolute的位置，相当于元素悬浮。离其最近的absolute或者relative层，没有的话就以body定位。margin也符号上述规则。
- fixed：
    生成绝对定位的元素，相对于浏览器窗口进行定位。元素的位置通过"left","top","right"以及"bottom"属性进行规定。可通过z-index进行层次分级。

### 4. border style

|dotted |solid |double |dashed|
|-------|------|-------|------| 
|点状   |实线   |双线   |虚线   |

### 5. background-attachment

滚动视觉差.

可以实现页面背景图固定的效果。

## 三、css优先级

### 1、相关概念

#### CSS继承

`CSS继承` 是从一个元素向其后代元素传递属性值所采用的机制。
确定应当向一个元素应用哪些值时，浏览器不仅要考虑继承，还要考虑声明的特殊性，另外需要考虑声明本身的来源。这个过程就称为层叠。

> 声明：CSS选择器后边大括号里的样式叫做声明。  
> 声明块： CSS选择器整个大括号叫做声明块。  
> 特殊性：一个元素可以被多少个规则设置，但是最终只有一个规则会起作用，那么该规则的特殊性最高，特殊性即CSS优先级。

### 2、优先级的计算

选择器的特殊值用4位标识，0，0，0，0 ，不同选择器对特殊值的影响如下：

|选择器                     |影响       |
|--------------------------|-----------|
|ID选择器的特殊性值         |加0,1,0,0  |
|类选择器、属性选择器或伪类  |加0,0,1,0  |
|元素和伪元素               |加0,0,0,1  |
|通配选择器*对特殊性没有贡献 |即0,0,0,0  |
|!important（权重）         |它没有特殊性值，但它的优先级是最高的，可以认为1,0,0,0,0|

### 3、浏览器比较不同规则的顺序

- 规则的权重（!important），加了权重的优先级最高
- 当权重相同的时候，会比较规则的特殊性，根据前面的优先级计算规则决定哪条规则起作用
- 当特殊性值也一样的时候，css规则会按顺序排序，后声明的规则优先级高，

> 后声明的规则优先级高

## 四、CSS实例

### 1. 纯CSS实现三角形

```css
.triangle{
    width:0;
    height:0;
    border-width:20px;
    border-style:solid dashed dashed dashed;
    border-color:#e66161 transparent transparent transparent;
}
```
> 利用了 CSS 中的 border 属性。

### 2. 对话框下边的三角形

利用旋转操作将正方形旋转。

### 3. 不定高元素垂直居中

- 使用：vertical-align:(对内部的文字起作用，内部不能是 div )
    - 外层 div，display: table-cell => 对 div 中的文字设置垂直居中，。
    - 外层 div，display: inline => 可以通过设置 line-height 改变 div 的高度。
    - 外层 div, display: inline-block => 设置 line-height 和 height 相同的时候，vertical-align 作用才会显现出。

- 外层 div设置为 relative，内层div 设置为 left:50%, top:50%, absolute，transform：translate(-50%, -50%), 或者使用 transform: translate3d(-50%, -50%, 0) 一样道理。
- 外层 div，display: -webkit-box; -webkit-box-algin: center; -webkit-bok-pack: center;（外层 div 里可以是文字，也可以是div）
    > -webkit-box-glign 只有 chrome,oprate 支持)