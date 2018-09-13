# 前端面试总结 - JavaScript

## 一、操作符

### 1、== && ===

例：value1 == value2 ， value3 === value4，

== ：（1）如果两个值类型相同，再进行三个等号(===)的比较。

         （2）如果两个值类型不同，也有可能相等，需根据以下规则进行类型转换在比较：

　　　　    1）如果一个是null，一个是undefined，那么相等。

　　　　    2）如果一个是字符串，一个是数值，把字符串转换成数值之后再进行比较。

===：（1）如果类型不同，则一定不相等。

           （2）如果两个都是数值并且是同一个值，那么相等。
    
           （3）如果一个是数值一个是 NaN，那么不相等。
    
           （4）如果都是true 或者 false 相等。
    
           （5）如果都是 null 或者 undefined，那么相等。注意，null == undefined => true, null === undefined => false.

1. string、number 等基础类型，== 与 === 的区别在于，== 会转换类型再进行比较，=== 不会转换类型比较。

2. array、object 等高级类型，== 与 === 没有区别。

3. 基础类型与高级类型比较，区别在于，== 将高级转换为基础类型，再进行比较，=== 因为类型不同，直接返回false

### 2、equals

JavaScript 中字符串没有 equals 方法，但是可以自己实现。

## 二、函数

### 1、ready() && onload()

- document.ready()

    是DOM结构绘制完成之后即可执行，不需要相关联资源下载完成，例如图片DOM结构绘制完成，而图片可能没有下载完成，其函数同样会执行。

- document.onload()

    相关资源都加载完毕之后，执行，一个页面中只能有一个onload

- load函数

    常用在图片的加载，比如 $('idName').load()，load同样是资源全部加载完成之后才会执行。

### 2、apply  &&  call  &&  bind

- 相同点：

  - 都是用来改变函数的this对象的指向的

  - 第一个参数都是this要指向的对象

- 都可以继续传递参数

```javascript
var xb = {
    name: '小冰',
    gender: '女',
    say: function(){
    alert(this.name + ',' + this.gender);
    }
}
var other = {
    name: '小东',
    gender: '男',
}

xb.say(); ===> 小冰，女
xb.say.call(other); ==> 小东，男
xb.say.apply(other);
xb.say.bind(other)();
```

#### 三个方法的不同点

- `call`和 `apply`方法，都是对函数的直接调用，但是 `bind()` 方法需要加上()来执行

- `call`和 `apply`方法传参的方法不同

  - xb.say.call(other,'斯坦福','3')。

  - xb.say.apply(other, 'sitanfu','third');   

- `bind` 返回的是方法

#### 实现 bind 方法

```javascript
if (!function() {}.bind) {
        Function.prototype.bind = function(context) {
        var self = this，
        args = Array.prototype.slice.call(arguments);
        return function() {
        return self.apply(context, args.slice(1));    
        }
        };
}
```

### 3、Typeof

Typeof 把参数的类型信息作为字符串返回。

可能的值有：

- number

- string

- boolean

- object

- function

- undefined

注意：typeof(null) 返回object。

### 4、定时器

- `setTimeout(.... , time)` 在指定的时间（time） 后调用函数或者计算表达式。

- `setInterval(code,millisec,lang)`, lang不是必需。会在指定的周期（millisec）不断调用函数（code），直到 clearInterval() 清除。

## 三、综合

## 1、垃圾回收机制

Js具有自动回收垃圾的机制，垃圾收集器会按照固定的时间间隔周期性执行。

- 标记清除

    工作原理：当变量进入环境时，将这个变量标记为“进入环境”，当变量离开环境时，则将其标记为“离开环境”。标记为“离开环境”的就会被回收。

- 引用计数

    跟踪记录每个值被引用的次数，当一个值被引用的次数为0时，垃圾收集器下次运行时就会将值回收。

### 2、内存泄漏

| 问题 | 解决办法|
|----------------|---------------|
|全局变量引起的内存泄漏|严格使用全局变量|
|闭包引起的内存泄漏。闭包可以维持函数内部变量，使其得不到释放|避免闭包，或者在外部事件处理函数中删除对DOM的引用|
|被遗忘的定时器或者回调函数|删除定时器|



### 3、JS对象属性遍历

1. 使用 Object.keys(objectName).forEach(function(element,index){ .... } 便利

2. Object.getOwnPropertyNames(), 返回一个数组，包含自身的所有属性（不包含symbol属性，但是包含不可枚举属性）。

3. Reflect.ownKeys(obj) ，包含所有属性，包含symbol属性和不可枚举属性

## 

### 4、cookies && storage

cookies、localStorage、sessionStorage都是在客户端以键值对存储的存储机制，并且只能将值存储为字符串。

`sessionStorage`常用操作方法：

- session.clear(), 清空

- session.setItem('key','value')

- session.getItem('key')

- session.removeItem('key')

- session.length,

||cookies | localStorage | sessionStorage|
|----|--------|--------------|---------------|
|初始化|客户端或服务器，服务器可使用Set-Cookies请求头|客户端|客户端|
|过期时间|手动设置|永不过期|当前页面刷新、关闭|
|与域名关联|是|否|否|
|容量|4kb|5mb|5mb|
|随请求发给服务器|是|否|否|


### 5、冒泡/捕获/事件委托/事件代理

`事件委托`就是利用事件冒泡，只指定一个事件处理程序，就可以管理某一类型的所有事件。

举例：

有三个同事预计会在周一收到快递。为签收快递，有两种办法：一是三个人在公司门口等快递；二是委托给前台MM代为签收。现实当中，我们大都采用委托的方案（公司也不会容忍那么多员工站在门口就为了等快递）。前台MM收到快递后，她会判断收件人是谁，然后按照收件人的要求签收，甚至代为付款。这种方案还有一个优势，那就是即使公司里来了新员工（不管多少），前台MM也会在收到寄给新员工的快递后核实并代为签收。

1. 现在委托前台的同事是可以代为签收的，即程序中的现有的dom节点是有事件的；

2. 新员工也是可以被前台MM代为签收的，即程序中新添加的dom节点也是有事件的。

发生事件的元素可以使用 `ev.target` 获取到，利用事件冒泡。

[参考文章](https://www.cnblogs.com/liugang-vip/p/5616484.html)

> 注意：$("ul").on("click","li",function(){});这样写有事件委托。$("ul li").on();这样写法则没有。


### 6、浏览器事件模型

1. 每个浏览器都有自己的事件模型，W3C为了兼顾标准，定义了三个阶段：捕获阶段，目标阶段，冒泡阶段。

2. elem.addEventListener("eventType", fn , boolean);

3. 参数说明: 事件类型，函数，true,表示在捕获阶段执行,false为在冒泡阶段执行(默认为false).

4. stopPropagation()可以阻止事件的传播，可以是捕获阶段也可以是冒泡阶段。

### 7、模块化

Commonjs、AMD、CMD、es6 modules

- CommonJS
  - 核心思想就是通过 require 方法来同步加载所要依赖的其他模块，然后通过 exports 或者 module.exports 来导出需要暴露的接口
  - 同步加载
  - 用于nodejs服务器端

- AMD规范
  - require.js
  - 非同步加载，允许指定回调函数
  - require([module],callback),引用函数
  - define(id, [dependences], callback), 定义函数
  - 支持 Commonjs 的导出方式
  - 只是提前加载所有依赖，不是按需加载

- CMD规范
  - sea.js
  - 按需加载 
  - 依赖spm打包
  - ES6模块化
  - import
  - 前端框架中常用

- es6 modules

### 8、闭包

简答的说，如果一个function能除了能访问它的参数、局部变量或函数之外，还能访问外部环境变量（包括全局变量、DOM、外部函数的变量或者函数），那么它就可以成为一个闭包。

```javascript
// 看代码猜结果:

function fun(n,o) {
  console.log(o);
  return {
    fun:function(m){
      return fun(m,n);
    }
  };
}

1. var a = fun(0); a.fun(1); a.fun(2); a.fun(3);//undefined,0,0,0
2. var b = fun(0).fun(1).fun(2).fun(3);//undefined，0,1,2,
3. var c = fun(0).fun(1); c.fun(2); c.fun(3);//undefined,0,1,1
```

> [参考文章](https://segmentfault.com/a/1190000009886713)

## 四、ES6 语法

### 1、新特性

1. Default Parameters（默认参数）

2. Template Literals （模板文本）

3. Multi-line Strings （多行字符串）

4. Destructuring Assignment （解构赋值）

5. Enhanced Object Literals （增强的对象文本）

6. Arrow Functions （箭头函数）

7. Promises

8. Block-Scoped Constructs Let and Const（块作用域构造Let and Const）

9. Classes（类）

10. Modules（模块）

## 五、前端框架


### 1、几个框架修改数据的不同

#### Vue

1. 创建一个数据对象，其中的数据可以自由更改。

> this.name = 'a' 赋值。this.name = 'b'，更改。

#### React

1. 创建一个状态对象，更改数据需要更多的操作。

2. 例如：this.status(...)

3. React之所以使用状态的方式，是为了方便在数据进行了改变之后，及时追踪和运行声明周期hook。

> this.state.name = 'a' 赋值。 this.setState({ name:'b' })。

### 2、Angular

#### 2.1 props  &&  state

1. props是不可变的，而state是可以根据用户的交互来改变的。

2. props不可改变是指在组件本身中修改，不过因为组件中的props本质作用是一种父级向子级传递数据的方式，所以可以在父组件中修改。

3. React 中更新组件的state，会导致重新渲染用户界面（不需要操作DOM），简单来说就是用户界面会随着state变化而变化

#### 2.2 路由实现原理

### 3、React

#### 虚拟DOM
React在Virtual DOM上实现了DOM diff算法，当数据更新时，会通过diff算法计算出相应的更新策略，尽量只对变化的部分进行实际的浏览器的DOM更新，而不是直接重新渲染整个DOM树，从而达到提高性能的目的。

#### Diff算法

> [相关网址](https://segmentfault.com/a/1190000010686582)

虚拟DOM树分层比较，忽略DOM节点跨层级的移动操作。React只会对相同颜色方框内的DOM节点进行比较，即同一个父节点下的所有子节点。当发现节点已经不存在，则该节点及其子节点会被完全删除掉，不会用于进一步的比较。这样只需要对树进行一次遍历，便能完成整个DOM树的比较。

如果真的发生跨级移动的话，React是删除原来的，再新建一个挂到DOM树上。

### 4、Vue

> 待补充

## 六、JQuery

### 1、jsonp

jsonp是JQuery 中解决跨域请求数据的一个解决办法。

```javascript
$.ajax({
  url: "http://localhost:9090/student",
  type: "GET", //只支持GET方法
  dataType: "jsonp",  //指定服务器返回的数据类型
  jsonpCallback: "showData",  //指定回调函数名称
  success: function (data) {
    console.info("调用success");
  }
});
```

## 七、JS实例

### 1、纯 JavaScript 验证手机号
```javascript
var phoneNumber;

phoneNumber  = document.getElementById("phone-number-input");

phoneRole = /^(1[1-9][0-9]{9})$/;

if (phoneRole.test(phoneNumber) == false) {

  alert("phone number is wrong");

}else {

  alert ("phone number is correct")

}
```

### 2、纯JS拼接URL

```javascript
export function encodeSearchParams(obj) {

  const params = []

  Object.keys(obj).forEach((key) => {

    let value = obj[key]
    
    // 如果值为undefined我们将其置空
    
    if (typeof value === 'undefined') {
    
      value = ''
    
    }
    
    // 对于需要编码的文本（比如说中文）我们要进行编码
    
    params.push([key, encodeURIComponent(value)].join('='))

  })

  return params.join('&')

}
```

### 3、js实现ajax方法

```javascript
function getAJAX(fn,url){

  var xhr = createXHR();

  xhr.open("GET",url,true);

  xhr.onreadystatechange =  function(){

    if(xhr.readyState == 4){//异步请求时的状态码4代表数据接收完毕

      if(xhr.status == 200){//HTTP的状态 成功
    
        var data = eval("(" + xhr.responseText + ")");
    
        fn(data);//实现函数的回调,将结果返回
      }
    }
  }
  xhr.send(null);
}
```