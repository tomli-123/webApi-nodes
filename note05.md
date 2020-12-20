# WebApi基本概念

## 为什么要学习WebApi?

> 我们前期学习的ECMAScript语法规范，都是在打基础。

想要做出好看的页面效果，就需要学习Web API，学了Web API之后就能操作页面元素了，才能做出来一些炫酷的效果。

## 什么是WebApi

API（Application Programming Interface,应用程序编程接口）,API是一些预先定义的方法，这些方法能够实现某些特定的功能，我们无须知道这些API的实现方式，但是我们需要知道这些API如何使用。

- 任何开发语言都会提供自己的API
- API的特征输入和输出(参数/返回值)

通俗的讲，API就是编程语言给我提供的一些工具，通过这些工具，我们可以非常轻易的完成一些功能。

```javascript
做饭需要一套做饭的工具：锅碗瓢盆
打仗需要一套打仗的工具：刀枪剑戟
找对象需一套找对象的工具：钱权颜缘

Web API: 浏览器提供的一套操作网页（web）的API（方法），通过这套API我们可以非常轻易的操作页面的元素和浏览器的一些功能。
```

**思考：我们学习Web API，我们该学什么？** 

![](images/javascript.png)

**ECMAScript - JavaScript的核心**

定义了JavaScript 的语法规范

JavaScript的核心，描述了语言的基本语法和数据类型，ECMAScript是一套标准，定义了一种语言的标准。与具体实现无关

**BOM - 浏览器对象模型**

一套操作浏览器功能的API

通过BOM可以操作浏览器窗口，比如：弹出框、控制浏览器跳转、获取分辨率等 

**DOM - 文档对象模型**

一套操作页面元素的API

DOM可以把HTML看做是文档树，通过DOM提供的API可以对树上的节点进行操作

# DOM-文档对象模型

## DOM基本概念

> DOM（Document Object Model）文档对象模型，是`W3C组织`推荐的一套用于处理`HTML`的标准`编程接口`。

DOM又称为文档树模型，因为整个HTML文档是一个树形的结构

![](images/1.png)

DOM中常见的概念

- 文档`document`：一个网页可以称为文档
- 节点`node`：网页中的所有内容都是节点（标签、属性、文本、注释等）
- 元素`element`：网页中的标签

## DOM初体验

> `document.getElementById("box")`的作用是根据页面中元素的id来获取元素

在DOM中，想要操作一个元素，首先需要先获取到这个元素才能进行操作。

```javascript
//功能：通过id获取元素
//参数：字符串类型的id值
//返回值：元素，如果id不存在，会返回null
var div = document.getElementById('main');

console.dir(div);
```

关于`console.log`和`console.dir`的区别

+ `console.log`打印一个元素的时候，是以标签的形式进行展示的
+ `console.dir`打印一个元素的时候，是以对象的形式进行展示的

在DOM中，页面标签的属性和DOM对象的属性是一一对应的，因此我们可以通过修改DOM对象的属性来修改标签的属性。

```html
//html内容
<div title="hehe" id="box">

<script>
// javascript代码
var div = document.getElementById('box');
div.title = "哈哈";
</script>

//结果：div标签的title属性就发生了更改
<div title="哈哈" id="box">
```



# 获取元素

## 使用getElementById的注意事项

+ 如果id不存在，会返回null
+ 在DOM中，`document.getElementById("box")`方法需要写在html内容的后面，保证页面加载完成之后才能获取到内容。
+ 部分浏览器，如果元素设置了id属性，可以直接使用（但是不是规范，不推荐）

**当getElementById返回null的时候，null.onclick就会报错**

```html
<!--没有id-->
<img src="images/1.jpg" alt="图破了" title="呵呵">

<script>
  //如果找不到，返回的是null，试图给null设置属性会报错
  var element = document.getElementById("img");
  element.title = "嘿嘿";//报错Uncaught TypeError: Cannot set property 'title' of null
</script>
```

[mdn地址](https://developer.mozilla.org/zh-CN/docs/Web/API/Document/getElementById)

## getElementsByTagName

> 通过标签名获取元素

```javascript
//参数：标签名
//返回值：一个伪数组， 伪数组不是数组，不能使用数组的方法，但是可以跟数组一样进行遍历和使用下标进行操作。
var divs = document.getElementsByTagName('div');
```

**注意：返回值有没有获取到元素，都是一个伪数组，即便元素只有一个**

## 缩小查找范围

1. `document.getElemntsByTagName("div")`表示获取页面中所有的div元素，范围太大了，可以使用`box.getElementsByTagName("div")`表示获取box中所有的div元素，范围更小。
2. `document.getElementById("demo")`表示获取页面中id为box的元素，没有`box.getElementById("demo")`这种用法。



# 注册事件

## 事件的基本使用

> 事件：触发-响应机制

事件三要素：

- 事件源:触发事件的元素
- 事件名称: click 点击事件
- 事件处理程序:事件触发后要执行的代码(函数形式)

注册事件的基本语法：

```javascript
var box = document.getElementById('box');
//on:当  click:点击   当按钮被点击的时候触发
box.onclick = function() {
  console.log('代码会在box被点击后执行');  
};
```

**注意：事件处理程序并不是立马执行，而是当事件触发的时候在会执行（浏览器会自动调用）**

练习：

```js
点击按钮，切换图片
```

## 修改标签的属性

> 在DOM中，页面标签的属性和DOM对象的属性是一一对应的，因此我们可以通过修改DOM对象的属性来修改标签的属性。

标签的alt，title，src，width，height等属性，可以直接通过对象进行修改。

**如果是class属性，在js中class是关键字，因此对应的是className属性**



练习：

```javascript
//1. 点击按钮，修改div的样式 -- 定义类名
//2. 点击按钮，div进行显示和隐藏（两个按钮） -- 预定义类名
//3. 点击按钮，div进行显示和隐藏（一个按钮） -- 预定义类名
```



【案例：二维码案例】

鼠标经过事件与鼠标离开事件

```javascript
onmouseover:当鼠标经过时触发
onmouseout:当鼠标离开时触发	
```



## 事件中的this

> 当在事件中表示当前元素的时候，可以使用this

```javascript
var btn = document.getElementById("btn");
btn.onclick = function() {
  //给 btn注册的事件，因此this表示btn
  this.value = "哈哈";
}
```

练习：

```javascript
//1. 给多个按钮注册点击事件，点击的那个变成红色
//2. 给多个按钮注册点击事件，当点击按钮，显示对应的图片 -- title属性记录图片src
```



## 阻止a标签跳转

> 对于a标签来说，默认的行为就是进行页面跳转，如果不想让a标签进行跳转，可以在注册事件中使用`return false`

```javascript
var link = document.getElementById("link");
link.onclick = function() {
  alert("呵呵");
  //阻止页面跳转
  return false;
}
```



# 标签的内容属性

> innerText和innerHTML属性都是用来获取和设置标签的内容的。但是二者还是有区别的。

> innerHTML可以用于获取和设置标签的所有内容，包括标签和文本内容

```
// innerHTML:内部的HTML
//  获取标签内容的时候，不管标签还是文本，都能获取到
//  innerHTML设置内容的时候，覆盖原来内容，标签也能生效，浏览器能解析这个标签。
```

> innerText可以用于获取和设置标签的文本内容，会丢弃掉标签

```
//innerText:内部文本
//  获取标签内容的时候，只会获取文本，标签扔掉了
//  设置标签内容的时候，覆盖原来内容，对标签进行转义（目的：把标签直接当文本来用）
```

二者的区别：

- innerHTML能够识别标签，标签能够生效
- innerText只识别文本，标签会被转义

## 案例：美女相册

```javascript
//1. 找对象
var imgs = document.getElementById("imgs");//ul
var links = imgs.getElementsByTagName("a");//所有的a标签
var bigImg = document.getElementById("bigImg");//大图片
var des = document.getElementById("des");

//2. 给所有的a标签注册点击事件
for(var i = 0; i < links.length; i++) {
  links[i].onclick = function () {

    //3. 修改大图片的src属性， this.href
    bigImg.src = this.href;

    //4. 修改p标签的内容, innerText:内部的文本
    des.innerText = this.title;

    //5. 阻止a跳转
    return false;
  }
}
```





# 表单属性操作

> 常见的表单属性有：disabled、type、value、checked、selected

对于disabled、checked、selected三个属性来说，比较特殊。

```javascript
在标签中，只要指定了disabled属性，无论有值没值，都代表这个input是被禁用的。注意，标签的disabled仅仅是默认值。
在DOM对象中，disabled的属性是一个布尔类型的属性，值只有true或者false
```

【案例：禁用文本框.html】

【案例：设置下拉框选中.html】

【案例：仿京东搜索文本框案例.html】

​		获得焦点与失去焦点案例

```javascript
onfocus:获得焦点时触发
onblur:失去焦点时触发	
```

【案例：表格全选案例.html】



# 样式操作（style属性）

> 标签不仅可以通过class属性操作样式，还可以通过style属性操作样式。同样的DOM对象可以通过className操作样式，也可以通过style属性操作样式。

```javascript
//1. style属性是一个对象，里面存储了所有行内样式对应的键值对。
//2. 如果样式的名字带了-，比如background-color,到了style对象中，变成了驼峰命名法，backgroundColor（因为-在js中不是一个合法的标识符）
//3. style属性只能获取和设置行内样式，在类样式中定义的样式通过style获取不到。
```

**style设置的样式是行内样式，因此优先级要高于className设置的样式**



## document常用属性：

```javascript
1. document.body  : body比较常用，并且在页面中时唯一的，因此可以使用document.body直接获取。
2. document.documentElement  : 可以获取html元素
3. document.head :  可以直接获取head元素
4. document.title :  可以直接获取title的文本
```

【案例：百度换肤】



# tab栏案例

> 排他思想：干掉所有人，复活我自己

【案例：排他思想.html】

【案例：获取当前元素的索引.html】

【案例：tab栏切换.html】



# 获取元素的方法

## 根据id获取

```javascript
//参数：元素的id
//返回值：一个元素，如果id不存在，返回null
document.getElementById("id");
```

## 根据标签名获取

```javascript
//参数：标签名
//返回值：伪数组，无论有几个元素，返回都是伪数组
document.getElementsByTagName("tagName");
box.getElementsByTagName("tagName");
```

## 根据类名获取

```javascript
//参数：字符串类型的类名
//返回值：伪数组
document.getElementsByClassName("class")
```

**注意：这个方法ie678不支持**

## 根据name获取

```javascript
//只适用于表单元素
var ps = document.getElementsByName("aa");
```

## 根据css选择器获取

```java
//参数：是一个css选择器，，   如果是类选择器，  .demo   如果是id选择器：  #aa
//返回值：只会返回一个对象，如果有很多个，会返回第一个
document.querySelector();

//参数：是一个css选择器
//返回值：会返回伪数组，不管有多少个，都会返回伪数组
document.querySelectorAll();
```



# 标签的自定义属性

> 我们之前讨论的属性，都是HTML规范中，标签本来就有的属性，对于标签自定义的一些属性，比较特殊。

在html页面中，定义一个自定义属性

```html
<div id="box" aa="bb"></div>
```

在对应的DOM对象中是不存在的，在DOM对象中只会存在固定的那些属性。

```javascript
var box = document.getElementById("box");
console.log(box.aa);//undefined
```

**attribute方法**

> attribute系列方法用于设置标签的属性，不管是自定义的还是固有的属性。

```
//获取标签的属性
box.getAttribute(name);
//设置标签的属性
box.setAttribute(name, value);
//移除标签的属性
box.removeAttribute(name);
```





# 节点操作

## 节点查找

### 孩子节点

```javascript
//childNodes:获取所有的孩子节点（包括了元素节点和其他很多类型的节点）
//children:获取所有的子元素（用途很广泛）
//firstChild //第一个子节点
//firstElementChild //第一个子元素
//lastChild //最后一个节点
//lastElementChild //最后一个子元素
```

### 兄弟节点

```javascript
//1. nextSibling:下一个兄弟节点
//2. nextElementSibling:下一个兄弟元素
//3. previousSibling//上一个兄弟节点
//4. previousElementSibling //上一个兄弟元素
```

### 父节点

```javascript
//1. parentNode:父节点
```

【案例：隔行变色】

【案例：表单校验】

### onkeydown与onkeyup事件

```javascript
1. onkeydown: 当键盘按下时触发的事件
2. onkeyup: 键盘弹起时触发的事件

注意：如果给文本框注册的是onkeydown事件，获取的value值是上一次的。
```



## 添加节点

### appendChild

语法：parent.appendChild(child)

parent: 调用者，父节点来调用

child:需要添加的那个孩子。

作用：把child添加到parent的孩子的最后面。

> 如果添加的是页面中本来就存在的元素，是一个剪切的效果，原来的就不在了。

```javascript
var demo = document.getElementById("demo");
var box = document.getElementById("box");
box.appendChild(demo);
```

### insertBefore

语法：parent.insertBefore(child, refChild);

parent:必须要父节点来调用

child：需要添加的那个节点

refChild:添加到哪一个节点的前面。

```javascript
var ul = document.getElementById("list");
var li = document.createElement("li");
li.innerHTML = "骥骥";
//就是添加到子节点的最前面。
ul.insertBefore(li, ul.children[0]);
```



## 克隆节点

语法：var newNode = node.cloneNode(deep)

功能：在内存中克隆一份节点

参数：deep

- false：默认值：是浅复制，只会复制标签，节点本身，不会复制节点的孩子。
- true:深度复制，会复制标签，还会复制标签的所有内容 --- **常用**

> 1. 克隆出来的节点跟原来的节点没有关系了，修改了也不会相互影响。
> 2. 如果克隆的节点带了id，我们需要给id重新设置一个值，不让id冲突



## 删除节点

语法：parent.removeChild(child);

功能：由父盒子调用，删除里面的一个子元素。

【案例：祝愿墙】 ---  ondblclick：双击的时候触发



## 创建节点（3种方式）

### document.write（基本不用）

可以生成新的节点，但是不推荐使用。***如果页面已经加载完成了，你还是用document.write写内容的话，会把之前的页面给覆盖掉*** 

原理：页面从上往下加载的时候，会开启一个文档流，当页面加载完，文档流就会关闭。

document.write的本意就是在文档流上写入内容。如果页面没加载完成，文档流还是开着的，document.write直接在这个文档流上写东西

如果页面加载完成了，还是用document.write写东西，会重新开启一个新的文档流，往新的文档流上写东西，旧的文档流就被新的文档流覆盖了。

### innerHTML

innerHTML也可以创建节点

> innerHTML创建节点的时候有一个特点，如果原来有内容的话，使用innerHTML会把原先的内容给干掉。
>
> 慎用：很容易出现性能效率问题。

### createElement

语法：var element = document.createElement("tagName");

作用：在内存里面创建了一个节点

返回：一个元素。 用途非常的广泛。

【案例：微博发布】



# 注册事件的两种方式

## on+事件名称

> onclick、onmouseover这种on+事件名称的方式注册事件几乎所有的浏览器都支持。

注册事件：

```javascript
box.onclick = function(){
	//事件处理程序	
}
```

移除事件：

```javascript
box.onclick = null;	
```

on+事件名称注册事件的缺点：

同一个元素同一类型的事件，只能注册一个，如果注册了多个，会出现覆盖问题。

## 注册事件的新方式

**addEventListener与removeEventListener**

> 现代浏览器支持的注册事件的新方式，这种方式注册的事件不会出现覆盖问题。

addEventListener的语法

```javascript
//第一个参数：事件的类型：click mouseover
//第二个参数：函数，监听者，每次点击，这个函数就执行。
//第三个参数：是否使用捕获，默认为false，表示冒泡
addEventListener(type, func, useCapture);
```

**tips：如果想要让你注册的事件能够移除，不能使用匿名函数。** 

```javascript
function fn1() {
    alert("hehe");
}
//如果想让注册的事件能移除，不能用匿名函数。
box.addEventListener("click", fn1, false);
```

removeEventListen的语法

```javascript
//第一个参数：参数类型
//第二个参数：要移除的那个函数
//第三个参数：false
removeEventListener(type, func, useCapture);
```

**attachEvent与detachEvent（了解）**

> IE678不支持addEventListener与removeEventListen两个方法，但是支持attachEvent与detachEvnet

attachEvent的用法：

```javascript
//type:事件类型   需要加上on   onclick  onmouseenter
//func:需要执行的那个事件
attachEvent(type, func)
```

detachEvent的用法

```javascript
//type:事件类型   需要加上on   onclick  onmouseenter
//func:需要执行的那个事件
detachEvent(type, func)
```



# 事件对象

## 事件对象的概述

> 在触发某个事件的时候，都会产生一个事件对象Event，这个对象中包含所有与事件相关的一些信息，包括触发事件的元素，事件的类型以及其他与事件相关的信息。

鼠标事件触发时，事件对象中会包含鼠标的位置信息。

键盘事件触发时，事件对象中会包含按下的键相关的信息。

```javascript
每一个事件在触发时，都会产生一个事件对象。
你见或者不见，我就在那里，不悲不喜。
你爱或者不爱，爱就在那里，不增不减。
你用或者不用，我都会给你，不离不弃。 
```

## 获取事件对象

> 既然事件对象中存储了这么多的信息，我们首先需要做的就是获取到这个事件对象。

获取事件对象非常的简单，只需要在注册事件的时候，指定一个形参即可。这个形参就是我们想要获取到的事件对象。

```javascript
btn.onclick = function(event){
    //event就是事件对象，里面包含了事件触发时的一些信息。
	console.log(event);
}
```

## 事件对象的常用属性

> 事件对象中有很多很多的属性，但是很多属性并不常用。我们经常用到的是***鼠标位置信息*** 和***键盘码***  相关的信息。

记录了鼠标位置信息的相关属性

```javascript
screenX与screenY：光标相对于屏幕左上角的水平位置与垂直位置。
clientX与clientY：光标相对于可视区左上角的水平位置和垂直位置。
pageX与pageY：光标相对于网页（文档document）左上角的水平位置与垂直位置（推荐使用）
```

【案例:让小天使飞.html】



记录了键盘码的属性

```javascript
获取键盘码: 在键盘事件中，通过e.keyCode可以获取到按下的键盘码
```

![键盘码](./images/keyCode.jpg)

【微博评论-添加回车发送功能】

## offset系列

### offsetHeight与offsetWidth

> offsetHeight与offsetWidth

```javascript
1. 获取的是元素真实的高度和宽度
2. 获取到的是数值类型，方便计算
3. offsetHeight与offsetWidth是只读属性，不能设置。
```

```javascript
获取宽度和高度offsetWidth与offsetHeight
```

### offsetParent

> parentNode和offsetParent

```javascript
1. parentNode始终是父元素
2. offsetParent是离当前元素最近的定位元素(absolute、relative)，如果没有，那就找body
```

### offsetLeft与offsetTop

> offsetLeft: 自身左侧到offsetParent左侧的距离；
>
> offsetTop:自身顶部到offsetParent顶部的距离；

```javascript
1.	元素自身与offsetParent真实的距离
2.	获取到的是数值类型，方便计算
3.	只读属性，只能获取，不能设置
```

 ![1](images/offset.png)

## 拖拽特效

【可拖拽的盒子.html】

## 放大镜效果（案例）

> 放大镜在开发中是一个很常见的特效，但是所有的放大镜的实现效果都是一样。

【案例-07-放大镜特效】

实现思路：

```javascript
1. 给box注册onmouseover事件，让big和mask显示
2. 给box注册onmouseout事件，让big和mask隐藏
3. 给box注册onmousemove事件，获取鼠标在box中的位置，让mask跟着移动
4. 限定mask的移动范围
5. 根据比例让bigImg跟着移动
```



# 事件流

## 事件冒泡

> 当一个元素的事件被触发时，同样的事件将会在该元素的所有祖先元素中依次被触发。这一过程被称为事件冒泡。

说白了就是：当我们触发了子元素的某个事件后，父元素对应的事件也会触发。

 ![bubble](./images/bubble.png)

## 事件捕获（了解）

> 事件捕获是火狐浏览器提出来的，IE678不支持事件捕获（基本上，我们都是用事件冒泡）
> 事件的处理将从DOM层次的根开始，而不是从触发事件的目标元素开始，事件被从目标元素的所有祖先元素依次往下传递

 ![capture](./images/capture.png)

```javascript
//当addEventListener第三个参数为true时，表示事件捕获
arr[i].addEventListener("click", function () {
    console.log(this);
},true);
```

## 事件的三个阶段

1. 事件的捕获阶段
2. 事件的目标阶段（触发自己的事件）
3. 事件的冒泡阶段

 ![three](./images/three.png)



事件有三个阶段，首先发生的是捕获阶段，然后是目标阶段，最后才是冒泡阶段，让`addEventLinstener`第三个参数为true时，表示该事件在捕获阶段发生，如果第三个参数为false，表示该事件在冒泡阶段发生。

## 阻止事件冒泡

> 通过e.stopPropagation()方法可以阻止事件冒泡

【案例：登录框】



## 事件补充：阻止浏览器默认行为

> 阻止浏览器默认行为除了使用 return false。
>
> 还可以通过 e.preventDefault() 可以阻止浏览器的默认行为



# 常见的事件整理

> 常见的鼠标事件

onmousedown:鼠标按下事件

onmouseup:鼠标弹起事件

onclick:单击事件

ondblclick：双击事件

onmouseover：鼠标经过事件

onmouseout：鼠标离开事件

onmousemove：鼠标移动事件

onfocus：鼠标获得焦点事件

onblur：鼠标失去焦点事件

> 常见的键盘事件

onkeydown:键盘按下时触发

onkeyup:键盘弹起时触发

> 对于鼠标事件，事件对象中有一系列的XY记录了鼠标的位置信息。
>
> 键盘事件中，事件对象有一个event.keyCode属性，记录了按下去的键的键盘码



# BOM

> BOM（Browser Object Model）：浏览器对象模型，提供了一套操作浏览器功能的工具。

 ![1](images\BOM.png)



BOM包含的内容很多，但是很多东西都不太常用，在BOM中需要大家掌握的就一个东西，那就是***定时器*** 。

## window对象

1. window对象是一个全局对象，也可以说是JavaScript中的顶级对象
2. 像document、alert()、console.log()这些都是window的属性，其实BOM中基本所有的属性和方法都是属性window的。
3. 所有定义在全局作用域中的变量、函数都会变成window对象的属性和方法
4. window对象下的属性和方法调用的时候可以省略window

### window.onload（掌握）

> window.onload事件会在窗体加载完成后执行，通常我们称之为入口函数。

```javascript
window.onload = function(){
	//里面的代码会在窗体加载完成后执行。
	//窗体加载完成包括文档树的加载、还有图片、文件的加载完成。
}
```

思考：一个页面能不能写两个window.onload?

## 延时器与定时器

### setTimeout

> setTimeout延时器可以在延迟时间到期后执行一个指定的函数。

设置延时器

```javascript
//语法：setTimeOut(callback, time);
//参数1：回调函数，时间到了就会执行。
//参数2：延时的时间
//返回：定时器的id，用于清除
//示例：
var timer = setTimeOut(function(){
	//1秒后将执行的代码。
}, 1000);
```

清除延时器

```javascript
//语法：clearTimeOut(timerId)
//参数：定时器id
//示例：
clearTimeOut(timer);//清除上面定义的定时器
```

### setInterval

> setInterval,方法重复调用一个函数或执行一个代码段，在每次调用之间具有固定的时间延迟。定时器除非清除，否则会一直执行下去。

设置定时器

```javascript
//语法：var intervalID = setInterval(func, delay);
//参数1：重复执行的函数
//参数2：每次延迟的毫秒数
//返回：定时器的id，用于清除
//示例：
var timer = setInterval(function(){
	//重复执行的代码。
}, 1000);
```

清除定时器

```javascript
//语法：clearInterval(intervalID)
//参数：定时器id
//示例：
clearInterval(timer);//清除上面定义的定时器
```

### 案例

【电子表】

【短信验证码案例.html】

## location对象

> location对象也是window的一个属性，location其实对应的就是浏览器中的地址栏。

### 常用属性和方法

> location.href:控制地址栏中的地址

```javascript
location.href = “http://www.baidu.com”;//让页面跳转到百度首页
console.log(window.location.search);//参数
```

> location.reload()：让页面重新加载

【案例：定时跳转.html】

## navigator对象

> window.navigator的一些属性可以获取客户端的一些信息

```javascript
//navigator.userAgent：浏览器版本
```

## history对象

history对象表示页面的历史

```javascript
//后退：
history.back();
history.go(-1);
//前进：
history.forward();
history.go(1);
```



# 动画函数封装

## 动画初体验-实现div到left=400的位置

```js
点击按钮，让div能够移动到400的位置，到达终点，清除定时器
```

## 动画初体验-让div做多个动画

```js
点击按钮1，让div能够移动到400的位置，到达终点，清除定时器
点击按钮2，让div能够移动到800的位置，到达终点，清除定时器
还要让div能够从800 移动到400的位置，到达终点，清除定时器
```

## 动画初体验-div到达终点

```js
让div移动到96px的位置，发现元素不能移动到终点位置
```

## 动画初体验-清除多个定时器

```js
点击元素多次，会发现元素会左右来回移动，到达不了终点。
```



# 短路运算

&&：短路与， 只要碰到了false，就会短路，短路后不会执行第二个表达式。

||：短路或，只要碰到了true就会短路，短路后不会执行第二个表达式。

**注意：&&和||的结果不一定是布尔类型，也可以是其他的类型**

**||经常用来给函数设置默认值**



# 轮播图

## 简单轮播图

```javascript
1. 结构分析
2. 按钮高亮以及排他
3. 移动图片：渐渐的移动图片，用到animate函数
```



## 左右焦点图

```javascript
1.结构分析
2.左右箭头的显示与隐藏
3.点击左箭头与右箭头（下标判断）
```



## 无缝轮播图

```javascript
1. 需要添加假图片
2. 真图片与假图片之间互相切换。
```



## 完整版轮播图

```js
1. js动态添加小圆点
2. js动态添加最后一张假图片
3. 实现左右焦点图 + 无缝滚动
4. 自动播放
5. 点击小圆点同步切换
6. 解决点击小圆点的bug
```





# 三大家族

## offset家族

> offset系列用于用于获取元素自身的大小和位置，在网页特效中有广泛应用
>
> offset系列主要有：offsetHeight、offsetWidth、offsetParent、offsetLeft、offsetTop

offsetHeight与offsetWidth

1. 获取的是元素真实的高度和宽度
2. 获取到的是数值类型，方便计算
3. offsetHeight与offsetWidth是只读属性，不能设置。

offsetHeight与offsetWidth的构成

	offsetHeight = height + paddnig + border
	
	offsetWidth = width + padding + border

 ![offset](images/offset.png)

## scroll家族

> scroll家族用来获取盒子内容的大小和位置
>
> scroll家族有：scrollWidth、scrollHeight、scrollLeft、scrollTop

1. scrollWidth与scrollHeight是盒子内容的真实的宽度和高度。与和盒子大小无关，仅仅与盒子的内容有关系。
2. scrollTop用于获取内容垂直滚动的像素数。如果没有滚动条，那么scrollTop值是0

 ![scroll](images/scroll.png)

onscroll事件，对于有滚动条的盒子，可以使用onscroll注册滚动事件，每滚动一像素，就会触发该事件。

```javascript
var box = doucment.getElementById(“box”);
box.onscroll = function(){
	//事件处理程序
}
```

获取页面被卷去的高度和宽度

> 通常来说，scroll家族用的最多的地方就是用来获取页面被卷去的宽度和高度，非常的常用

页面被卷去的高度和宽度

```javascript
window.onscroll = function() {
  var scrollTop = window.pageYOffset
  var scrollLeft = window.pageXOffset
}
```

【仿腾讯固定导航案例.html】

## client家族

> client家族用于获取盒子可视区的大小
>
> client家族有clientWidth、clientHeight、clientLeft、clientTop

clietnWidth: 获取内容和padding的大小

clientHeight:获取内容与padding的大小

> clientTop与clientLeft

**clientTop**与**clientLeft** 完全没有用，他们就是borderTop与borderLeft

 ![client1](images/client1.png)

> 三大家族对比

 ![client](images/client.png)



> onresize事件：onresize事件会在窗口被调整大小的时候发生。

```javascript
window.onresize = function(){
	//事件处理程序
    var width = window.innerWidth;
    var height = window.innerHeight
}
```





# 移动端

## 类名操作

> 推荐：classList是一个集合，会存储某个元素上所有的类名，使用classList来替代className操作class类

```javascript
//添加类
node.classList.add("classname");
//移除类
node.classList.remove("classname");
//切换类
node.classList.toggle("classname");
//判断类
node.classList.contains("classname");
```

## touch事件

移动端新增了4个与手指触摸相关的事件。

```javascript
//touchstart:手指放到屏幕上时触发
//touchmove:手指在屏幕上滑动式触发（会触发多次）
//touchend:手指离开屏幕时触发
//touchcancel:系统取消touch事件的时候触发,比如电话
```

每个触摸事件被触发后，会生成一个event对象，event对象中`changedTouches`会记录手指滑动的信息。

```javascript
e.touches;//当前屏幕上的手指
e.targetTouches;//当前dom元素上的手指。
e.changedTouches;//触摸时发生改变的手指。(重点)
```

这些列表里的每次触摸由touch对象组成，touch对象里包含着触摸信息，主要属性如下

```javascript
clientX / clientY: //触摸点相对浏览器窗口的位置
pageX / pageY:     //触摸点相对于页面的位置
```
