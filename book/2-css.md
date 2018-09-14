## 一、CSS属性

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

## 二、css优先级

## 三、CSS3

### 1. flex-box布局

是CSS3中的一种新的布局模式，是可以自动调整子元素的高和宽，来很好的填充任何不同屏幕大小的显示设备中的可用显示空间。
收缩内容防止内容溢出，确保元素拥有恰当的行为的布局方式，例如：对齐方式，排列方向，排列顺序。

> [参考文章](http://www.css88.com/archives/5726)

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

- 外层 div设置为relative，内层div absolute，transform：translate(-50%, -50%), 或者使用 transform: translate3d(-50%, -50%, 0) 一样道理。
- 外层 div，display: -webkit-box; -webkit-box-algin: center; -webkit-bok-pack: center;（外层 div 里可以是文字，也可以是div）
    > -webkit-box-glign 只有 chrome,oprate 支持)

## 三、Less  &&  Sass

### less

- 变量、Mixin、函数等特性
- lessc 命令进行编译
- 运行在node.js端或者浏览器端，浏览器加载less.js

### sass

- 变量，嵌套，混合
- sass命令进行编译