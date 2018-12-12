---
title: 龙湖地产
sidebar: auto
sidebarDepth: 2
---
# 龙湖地产笔试+面试

##  龙湖笔试题经典案例
####  1.块级和行内元素元素有哪些，它们有什么区别？
> 首先：CSS规范规定，每个元素都有display属性，确定该元素的类型，每个元素都有默认的display值，如div的display默认值为“block”，则为“块级”元素；span默认display属性值为“inline”，是“行内”元素。
- 行内元素有：a b span img input select strong（强调的语气）
- 块级元素有：div ul ol li dl dt dd h1 h2 h3 h4…p
- 它们的区别：
  - 行内元素与块级函数可以相互转换，通过修改display属性值来切换块级元素和行内元素，行内元素display：inline，块级元素display：block。
  - 行内元素和其他行内元素都会在一条水平线上排列，都是在同一行的；块级元素却总是会在新的一行开始排列，各个块级元素独占一行，垂直向下排列，若想使其水平方向排序，可使用左右浮动（float：left/right）让其水平方向排列。
  - 行内元素不可以设置宽高，宽度高度随文本内容的变化而变化，但是可以设置行高（line-height），同时在设置外边距margin上下无效，左右有效，内填充padding上下无效，左右有效；块级元素可以设置宽高，并且宽度高度以及外边距，内填充都可随意控制。        
  - 块级元素可以包含行内元素和块级元素，还可以容纳内联元素和其他元素；行内元素不能包含块级元素，只能容纳文本或者其他行内元素。

#### 2. 为什么要少用Iframe?
##### 一、使用iframe的优缺点
- 优点:
  - 程序调入静态页面比较方便;
  - 页面和程序分离;
- 缺点：
  - iframe有不好之处：样式/脚本需要额外链入，会增加请求。另外用js防盗链只防得了小偷，防不了大盗。
  - iframe好在能够把原先的网页全部原封不动显示下来,但是如果用在首页,是搜索引擎最讨厌的.那么你的网站即使做的在好,也排不到好的名次! 
  - 如果是动态网页，用include还好点！
  - 但是必须要去除他的\<html>\<head>\<title>\<body>标签！ 
  - 框架结构有时会让人感到迷惑，特别是在多个框架中都出现上下、左右滚动条的时候。这些滚动条除了会挤占已经特别有限的页面空间外，还会分散访问者的留心力。访问者遇到这种站点往往会立刻转身离开。他们会想，既然你的主页如此混乱，那么站点的其他部分也许更不值得阅读。
  - 链接导航疑问。运用框架结构时，你必须保证正确配置所有的导航链接，如不然，会给访问者带来很大的麻烦。比如被链接的页面出现在导航框架内，这种情况下访问者便被陷住了，因为此时他没有其他地点可去。
  - 调用外部页面,需要额外调用css,给页面带来额外的请求次数;

##### 二、为什么少用iframe
>iframes 提供了一个简单的方式把一个网站的内容嵌入到另一个网站中。但我们需要慎重的使用iframe。iframe的创建比其它包括scripts和css的 DOM 元素的创建慢了 1-2 个数量级。
使用 iframe 的页面一般不会包含太多 iframe，所以创建 DOM 节点所花费的时间不会占很大的比重。但带来一些其它的问题：onload 事件以及连接池(connection pool)。
1. Iframes 阻塞页面加载
   - 及时触发 window 的 onload 事件是非常重要的。onload 事件触发使浏览器的 “忙” 指示器停止，告诉用户当前网页已经加载完毕。当 onload 事件加载延迟后，它给用户的感觉就是这个网页非常慢。window 的 onload 事件需要在所有 iframe 加载完毕后(包含里面的元素)才会触发。在 Safari 和 Chrome 里，通过 JavaScript 动态设置 iframe 的 SRC 可以避免这种阻塞情况。
1. 唯一的连接池
    - 浏览器只能开少量的连接到web服务器。比较老的浏览器，包含 Internet Explorer 6 & 7 和 Firefox 2，只能对一个域名(hostname)同时打开两个连接。这个数量的限制在新版本的浏览器中有所提高。Safari 3+ 和 Opera 9+ 可同时对一个域名打开 4 个连接，Chrome 1+, IE 8 以及 Firefox 3 可以同时打开 6 个。你可以通过这篇文章查看具体的数据表：Roundup on Parallel Connections。
    - 有人可能希望 iframe会有自己独立的连接池，但不是这样的。绝大部分浏览器，主页面和其中的 iframe 是共享这些连接的。这意味着 iframe 在加载资源时可能用光了所有的可用连接，从而阻塞了主页面资源的加载。如果 iframe 中的内容比主页面的内容更重要，这当然是很好的。但通常情况下，iframe 里的内容是没有主页面的内容重要的。这时 iframe 中用光了可用的连接就是不值得的了。一种解决办法是，在主页面上重要的元素加载完毕后，再动态设置 iframe 的 SRC。
1. 美国前 10 大网站都使用了iframe
    - 大部分情况下，他们用它来加载广告。这是可以理解的，也是一种符合逻辑的解决方案，用一种简单的办法来加载广告服务。但请记住，iframe 会给你的页面性能带来冲击。只要可能，不要使用 iframe。当确实需要时，谨慎的使用他们。

#### 3. 写画如下代码的页面展示效果图，c盒子有position：relative和没position值有什么区别？
```
<head>
    <style>
        .box {
            width: 200px;
            height: 200px;
            display: inline-block;
        }
        .a {
            background-color: tan;
            position: absolute;
        }
        .b {
            background-color: blue;
            position: absolute;
        }
        .c {
            background-color: green;
            position: relative;
        }
    </style>
</head>
<body>
    <div class="a box"></div>
    <div class="b box"></div>
    <div class="c box"></div>
</body>
```

#### 4. call和apply的区别列举使用方法
>ECMAScript中的函数是对象，因此函数也有属性与方法。每个函数都包含两个非继承而来的方法：apply()和call()。这两个方法的用途都是在特定的作用域中调用函数，实际上等于设置函数体内this的对象的值。

##### 一、apply()方法
apply()方法接受两个两个参数：一个是在其中运行函数的作用域，另一个是参数数组。其中第二个参数可以是Array的实例，也可以是arguments对象
```
function sum(num1,num2){
    return num1 + num2;
}

function callsum1(num1,num2){
    return sum.apply(this,[num1,num2]);//传入数组
}
function callsum2(num1,num2){
    return sum.apply(this,arguments);//传入arguments对象
}

alert(callsum1(10,10));//20
alert(callsum2(10,10));//20
```
##### 二、call()方法
call()方法与apply()方法的作用相同，区别仅仅在于接受参数的方式不同。对于call()方法而言，第一个参数是this值没有变化，变化的是其余参数都直接传递给函数。也即，在使用call()方法时，传递给函数的参数必须逐个列举出来，如下
```
function sum(num1,num2){
    return num1 + num2;
}

function callsum(num1,num2){
    return sum.call(this, num1, num2); 
}

alert(callsum(10,10));//20
```
##### 三、传参并非apply()和call()的真正存在意义，其真正强大地方在于能够扩充函数的作用域。使用此两种方法来扩充作用域最大好处就在于对象不需要与方法有任何耦合关系
```
function sayColor(sPrefix,sSuffix) {
    alert(sPrefix + this.color + sSuffix);
};
 
var obj = new Object();
obj.color = "blue";
 
sayColor.call(obj, "The color is ", "a very nice color indeed.");
```
在这个例子中，函数 sayColor() 在对象外定义，即使它不属于任何对象，也可以引用关键字 this。对象 obj 的 color 属性等于 blue。调用 call() 方法时，第一个参数是 obj，说明应该赋予 sayColor() 函数中的 this 关键字值是 obj。第二个和第三个参数是字符串。它们与 sayColor() 函数中的参数 sPrefix 和 sSuffix 匹配，最后生成的消息 "The color is blue, a very nice color indeed." 将被显示出来。

```
function sayColor(sPrefix,sSuffix) {
    alert(sPrefix + this.color + sSuffix);
};
 
var obj = new Object();
obj.color = "blue";
 
sayColor.apply(obj, new Array("The color is ", "a very nice color indeed."));
```
这个例子与前面的例子相同，只是现在调用的是 apply() 方法。调用 apply() 方法时，第一个参数仍是 obj，说明应该赋予 sayColor() 函数中的 this 关键字值是 obj。第二个参数是由两个字符串构成的数组，与 sayColor() 函数中的参数 sPrefix 和 sSuffix 匹配，最后生成的消息仍是 "The color is blue, a very nice color indeed."，将被显示出来。

#### 5. 写出下面代码的输入值
```
5.1 (function(x){
    delete x;
    return x;
})(1);

5.2 var y = 1, x = y = typeof x;
console.log(x);

5.3 (function f(f){
    return typeof f();
})(function(){ 
    return 1; 
});

5.4 !!typeof(null)
```

#### 6.写出如下代码的运行结果
```
function Fun(){
    var printNum= function(){
        console.log(1);
    }
    return this;
}
Fun.printNum = function(){
    console.log(2);
}
Fun.prototype.printNum = function(){
    console.log(3);
}
var printNum = function(){
    console.log(4);
}
function printNum (){
    console.log(5);
}
Fun().printNum();
printNum();
Fun();
printNum();
new Fun().printNum();
new new Fun().printNum();
```

#### 7. var arrs = [1,2,[3,4,[5]],6,[7,[8,9,[10,11,[12]]]]]请写一个方法把数组拍扁成普通数组。
>提示：递归函数
```
let arrs = [1,2,[3,4,[5]],6,[7,[8,9,[10,11,[12]]]]]
let newArrs = [];
let recursive = (arr) => {
    arr.forEach((v,i) => {
        if(v instanceof Array){
            recursive(v);
        }else{
            newArrs.push(v);
        }
    })
}
recursive(arrs);
console.log(newArrs); //[1,2,3,4,5,6,7,8,9,10,11,12]
```

#### 8. 写一写你常用和重要的es6知识点
##### 1. 变量声明let和const
我们都是知道在ES6以前，var关键字声明变量。无论声明在何处，都会被视为声明在函数的最顶部(不在函数内即在全局作用域的最顶部)。这就是函数变量提升例如:

```
function aa() {
    if(bool) {
        var test = 'hello man'
    } else {
        console.log(test)
    }
}
```
以上的代码实际上是：

```
function aa() {
    var test // 变量提升
    if(bool) {
        test = 'hello man'
    } else {
        //此处访问test 值为undefined
        console.log(test)
    }
    //此处访问test 值为undefined
}
```
所以不用关心bool是否为true or false。实际上，无论如何test都会被创建声明。

接下来ES6主角登场：

我们通常用let和const来声明，let表示变量、const表示常量。let和const都是块级作用域。怎么理解这个块级作用域？

在一个函数内部

在一个代码块内部

说白了 {}大括号内的代码块即为let 和 const的作用域。

看以下代码：

```
function aa() {
    if(bool) {
        let test = 'hello man'
    } else {
        //test 在此处访问不到
        console.log(test)
    }
}
```
let的作用域是在它所在当前代码块，但不会被提升到当前函数的最顶部。

再来说说const。

 const name = 'lux';
    name = 'joe' //再次赋值此时会报错
    
说一道面试题

```
var funcs = []
for (var i = 0; i < 10; i++) {
    funcs.push(function() { console.log(i) })
}
funcs.forEach(function(func) {
    func()
})
```
这样的面试题是大家常见，很多同学一看就知道输出 10 十次，
但是如果我们想依次输出0到9呢？两种解决方法。直接上代码。

```
// ES5告诉我们可以利用闭包解决这个问题
    var funcs = []
    for (var i = 0; i < 10; i++) {
        func.push((function(value) {
            return function() {
                console.log(value)
            }
        }(i)))
    }
    // es6
    for (let i = 0; i < 10; i++) {
        func.push(function() {
            console.log(i)
        })
    }
```
达到相同的效果，es6简洁的解决方案是不是更让你心动！！！

##### 2.模板字符串
es6模板字符简直是开发者的福音啊，解决了ES5在字符串功能上的痛点。

第一个用途，基本的字符串格式化。将表达式嵌入字符串中进行拼接。用${}来界定。
```
//es5 
var name = 'lux'
console.log('hello' + name)
//es6
const name = 'lux'
console.log(`hello ${name}`) //hello lux
```
第二个用途，在ES5时我们通过反斜杠`\`来做多行字符串或者字符串一行行拼接。ES6反引号(``)直接搞定。

```
// es5
var msg = "Hi \
man!"
// es6
const template = `<div>
    <span>hello world</span>
</div>`
```
对于字符串es6当然也提供了很多厉害的方法。说几个常用的。

```
// 1.includes：判断是否包含然后直接返回布尔值
let str = 'hahay'
console.log(str.includes('y')) // true
// 2.repeat: 获取字符串重复n次
let s = 'he'
console.log(s.repeat(3)) // 'hehehe'
//如果你带入小数, Math.floor(num) 来处理
```

##### 3.函数
 - 函数默认参数

在ES5我们给函数定义参数默认值是怎么样？
```
function action(num) {
    num = num || 200
    //当传入num时，num为传入的值
    //当没传入参数时，num即有了默认值200
    return num
}
```
但细心观察的同学们肯定会发现，num传入为0的时候就是false， 此时num = 200 与我们的实际要的效果明显不一样

ES6为参数提供了默认值。在定义函数时便初始化了这个参数，以便在参数没有被传递进去时使用。
```
function action(num = 200) {
    console.log(num)
}
action() //200
action(300) //300
```
 - 箭头函数

ES6很有意思的一部分就是函数的快捷写法。也就是箭头函数。

箭头函数最直观的三个特点。

不需要function关键字来创建函数，
省略return关键字，
继承当前上下文的 this 关键字
```
//例如：
    [1,2,3].map( x => x + 1 )

//等同于：
    [1,2,3].map((function(x){
        return x + 1
    }).bind(this))
```
说个小细节。

当你的函数有且仅有一个参数的时候，是可以省略掉括号的。当你函数返回有且仅有一个表达式的时候可以省略{}；例如:
```
var people = name => 'hello' + name
//参数name就没有括号
作为参考

var people = (name, age) => {
    const fullName = 'h' + name
    return fullName
} 
//如果缺少()或者{}就会报错
```
##### 4.拓展的对象功能
- 对象初始化简写

ES5我们对于对象都是以键值对的形式书写，是有可能出现键值对重名的。例如：
```
function people(name, age) {
    return {
        name: name,
        age: age
    };
}
```
键值对重名，ES6可以简写如下：
```
function people(name, age) {
    return {
        name,
        age
    };
}
```
ES6 同样改进了为对象字面量方法赋值的语法。ES5为对象添加方法：
```
const people = {
    name: 'lux',
    getName: function() {
        console.log(this.name)
    }
}
```
ES6通过省略冒号与 function 关键字，将这个语法变得更简洁
```
const people = {
    name: 'lux',
    getName () {
        console.log(this.name)
    }
}
```
ES6 对象提供了Object.assign()这个方法来实现浅复制。Object.assign()可以把任意多个源对象自身可枚举的属性拷贝给目标对象，然后返回目标对象。第一参数即为目标对象。在实际项目中，我们为了不改变源对象。一般会把目标对象传为{}

```const obj = Object.assign({}, objA, objB)```

##### 5.更方便的数据访问--解构
数组和对象是JS中最常用也是最重要表示形式。为了简化提取信息，ES6新增了解构，这是将一个数据结构分解为更小的部分的过程

ES5我们提取对象中的信息形式如下：

```
const people = {
    name: 'lux',
    age: 20
}
const name = people.name
const age = people.age
console.log(name + ' --- ' + age)
```
是不是觉得很熟悉，没错，在ES6之前我们就是这样获取对象信息的，一个一个获取。现在，解构能让我们从对象或者数组里取出数据存为变量，例如

```
//对象
const people = {
    name: 'lux',
    age: 20
}
const { name, age } = people
console.log(`${name} --- ${age}`)
//数组
const color = ['red', 'blue']
const [first, second] = color
console.log(first) //'red'
console.log(second) //'blue'
```
##### 6.Spread Operator 展开运算符
ES6中另外一个好玩的特性就是Spread Operator 也是三个点儿...接下来就展示一下它的用途。

- 组装对象或者数组

```
//数组
const color = ['red', 'yellow']
const colorful = [...color, 'green', 'pink']
console.log(colorful) //[red, yellow, green, pink]

//对象
const alp = { fist: 'a', second: 'b'}
const alphabets = { ...alp, third: 'c' }
console.log(alphabets) //{ "fist": "a", "second": "b", "third": "c"
}
```
有时候我们想获取数组或者对象除了前几项或者除了某几项的其他项

```
const number = [1,2,3,4,5]
const [first, ...rest] = number
console.log(rest) //2,3,4,5
//对象
const user = {
    username: 'lux',
    gender: 'female',
    age: 19,
    address: 'peking'
}
const { username, ...rest } = user
console.log(rest) //{"address": "peking", "age": 19, "gender": "female"
}
```
对于 Object 而言，还可以用于组合成新的 Object 。(ES2017 stage-2 proposal) 当然如果有重复的属性名，右边覆盖左边

```
const first = {
    a: 1,
    b: 2,
    c: 6,
}
const second = {
    c: 3,
    d: 4
}
const total = { ...first, ...second }
console.log(total) // { a: 1, b: 2, c: 3, d: 4 }
```
##### 7.import 和 export
- import导入模块、export导出模块

```
//全部导入
import people from './example'

//有一种特殊情况，即允许你将整个模块当作单一对象进行导入
//该模块的所有导出都会作为对象的属性存在
import * as example from "./example.js"
console.log(example.name)
console.log(example.age)
console.log(example.getName())

//导入部分
import {name, age} from './example'

// 导出默认, 有且只有一个默认
export default App

// 部分导出
export class App extend Component {};
```
以前有人问我，导入的时候有没有大括号的区别是什么。下面是我在工作中的总结：

```
1.当用export default people导出时，就用 import people 导入（不带大括号）

2.一个文件里，有且只能有一个export default。但可以有多个export。

3.当用export name 时，就用import { name }导入（记得带上大括号）

4.当一个文件里，既有一个export default people, 又有多个export name 或者 export age时，导入就用 import people, { name, age } 

5.当一个文件里出现n多个 export 导出很多模块，导入时除了一个一个导入，也可以用import * as example

```
##### 8. Promise
在promise之前代码过多的回调或者嵌套，可读性差、耦合度高、扩展性低。通过Promise机制，扁平化的代码机构，大大提高了代码可读性；用同步编程的方式来编写异步代码，保存线性的代码逻辑，极大的降低了代码耦合性而提高了程序的可扩展性。

说白了就是用同步的方式去写异步代码。

- 发起异步请求
```
 fetch('/api/todos')
      .then(res => res.json())
      .then(data => ({ data }))
      .catch(err => ({ err }));
```
今天看到一篇关于面试题的很有意思。

```
setTimeout(function() {
    console.log(1)
}, 0);
new Promise(function executor(resolve) {
    console.log(2);
    for( var i=0 ; i<10000 ; i++ ) {
        i == 9999 && resolve();
    }
    console.log(3);
}).then(function() {
    console.log(4);
});
    console.log(5);
```
Excuse me？这个前端面试在搞事！

当然以上promise的知识点，这个只是冰山一角。需要更多地去学习应用。

##### 9.Generators
生成器（ generator）是能返回一个迭代器的函数。生成器函数也是一种函数，最直观的表现就是比普通的function多了个星号*，在其函数体内可以使用yield关键字,有意思的是函数会在每个yield后暂停。

这里生活中有一个比较形象的例子。咱们到银行办理业务时候都得向大厅的机器取一张排队号。你拿到你的排队号，机器并不会自动为你再出下一张票。也就是说取票机“暂停”住了，直到下一个人再次唤起才会继续吐票。

OK。说说迭代器。当你调用一个generator时，它将返回一个迭代器对象。这个迭代器对象拥有一个叫做next的方法来帮助你重启generator函数并得到下一个值。next方法不仅返回值，它返回的对象具有两个属性：done和value。value是你获得的值，done用来表明你的generator是否已经停止提供值。继续用刚刚取票的例子，每张排队号就是这里的value，打印票的纸是否用完就这是这里的done。

```
// 生成器
    function *createIterator() {
        yield 1;
        yield 2;
        yield 3;
    }

    // 生成器能像正规函数那样被调用，但会返回一个迭代器
    let iterator = createIterator();

    console.log(iterator.next().value); // 1
    console.log(iterator.next().value); // 2
    console.log(iterator.next().value); // 3
```
那生成器和迭代器又有什么用处呢？

围绕着生成器的许多兴奋点都与异步编程直接相关。异步调用对于我们来说是很困难的事，我们的函数并不会等待异步调用完再执行，你可能会想到用回调函数，（当然还有其他方案比如Promise比如Async/await）。

生成器可以让我们的代码进行等待。就不用嵌套的回调函数。使用generator可以确保当异步调用在我们的generator函数运行一下行代码之前完成时暂停函数的执行。

那么问题来了，咱们也不能手动一直调用next()方法，你需要一个能够调用生成器并启动迭代器的方法。就像这样子的

```
function run(taskDef) { //taskDef即一个生成器函数

        // 创建迭代器，让它在别处可用
        let task = taskDef();

        // 启动任务
        let result = task.next();

        // 递归使用函数来保持对 next() 的调用
        function step() {

            // 如果还有更多要做的
            if (!result.done) {
                result = task.next();
                step();
            }
        }

        // 开始处理过程
        step();

    }
```
生成器与迭代器最有趣、最令人激动的方面，或许就是可创建外观清晰的异步操作代码。你不必到处使用回调函数，而是可以建立貌似同步的代码，但实际上却使用 yield 来等待异步操作结束。

##### 总结
ES6的特性远不止于此，但对于我们日常的开发开说。这已经是够够的了。还有很多有意思的方法。比如findIndex...等等。包括用set来完成面试题常客数组去重问题。我和我的小伙伴们都惊呆了!

#### 9. 同步和异步的概念和区别
你应该知道，javascript语言是一门“单线程”的语言，不像java语言，类继承Thread再来个thread.start就可以开辟一个线程，所以，javascript就像一条流水线，仅仅是一条流水线而已，要么加工，要么包装，不能同时进行多个任务和流程。

那么这里说的同步和异步到底是什么呢？如果你真的不懂，我希望你认真读完这篇文章。其实我个人觉得js官方的文档在使用两个词的时候并不准确，包括很多其他词汇，都只是听起来高深，但实际应用好像跟这些词没半毛钱关系。例如“事件委托”这个词，不知道的人乍一看谁又能说出“事件委托”是什么意思？委托什么事件？怎么个委托，我看不如干脆就叫“事件在外层元素中的捕获”，虽然长一点，一下就能看懂。

回归正轨，“同步”——一下就让人想到“一起”这个词；“异步”呢，从字面来讲，好像是在不同的（异）的ways上do something，那首先想到的词可能是“一边...一边...”,比如‘小明一边吃雪糕一边写作业’，这完全没毛病，雪糕吃完了，作业也写完了，这就是异步？那就大错特错了！

其实同步和异步，无论如何，做事情的时候都是只有一条流水线（单线程），同步和异步的差别就在于这条流水线上各个流程的执行顺序不同。

最基础的异步是setTimeout和setInterval函数，很常见，但是很少人有人知道其实这就是异步，因为它们可以控制js的执行顺序。我们也可以简单地理解为：可以改变程序正常执行顺序的操作就可以看成是异步操作。如下代码：
```
<script type="text/javascript">
        console.log( "1" );
        setTimeout(function() {
            console.log( "2" )
        }, 0 );
        setTimeout(function() {
            console.log( "3" )
        }, 0 );
        setTimeout(function() {
            console.log( "4" )
        }, 0 );
        console.log( "5" );
</script>
```
输出顺序是什么呢？

可见，尽管我们设置了setTimeout（function，time）中的等待时间为0，结果其中的function还是后执行。

火狐浏览器的api文档有这样一句话：Because even though setTimeout was called with a delay of zero, it's placed on a queue and scheduled to run at the next opportunity, not immediately. Currently executing code must complete before functions on the queue are executed, the resulting execution order may not be as expected.

意思就是：尽管setTimeout的time延迟时间为0，其中的function也会被放入一个队列中，等待下一个机会执行，当前的代码（指不需要加入队列中的程序）必须在该队列的程序完成之前完成，因此结果可能不与预期结果相同。

这里说到了一个“队列”（即任务队列），该队列放的是什么呢，放的就是setTimeout中的function，这些function依次加入该队列，即该队列中所有function中的程序将会在该队列以外的所有代码执行完毕之后再以此执行，这是为什么呢？因为在执行程序的时候，浏览器会默认setTimeout以及ajax请求这一类的方法都是耗时程序（尽管可能不耗时），将其加入一个队列中，该队列是一个存储耗时程序的队列，在所有不耗时程序执行过后，再来依次执行该队列中的程序。

又回到了最初的起点——javascript是单线程。单线程就意味着，所有任务需要排队，前一个任务结束，才会执行后一个任务。如果前一个任务耗时很长，后一个任务就不得不一直等着。于是就有一个概念——任务队列。如果排队是因为计算量大，CPU忙不过来，倒也算了，但是很多时候CPU是闲着的，因为IO设备（输入输出设备）很慢（比如Ajax操作从网络读取数据），不得不等着结果出来，再往下执行。于是JavaScript语言的设计者意识到，这时主线程完全可以不管IO设备，挂起处于等待中的任务，先运行排在后面的任务。等到IO设备返回了结果，再回过头，把挂起的任务继续执行下去。

于是，所有任务可以分成两种，一种是同步任务（synchronous），另一种是异步任务（asynchronous）。同步任务指的是，在主线程上排队执行的任务，只有前一个任务执行完毕，才能执行后一个任务；异步任务指的是，不进入主线程、而进入"任务队列"（task queue）的任务，只有等主线程任务执行完毕，"任务队列"开始通知主线程，请求执行任务，该任务才会进入主线程执行。

##### 具体来说，异步运行机制如下：

 1. 所有同步任务都在主线程上执行，形成一个执行栈（execution context stack）。
 1. 主线程之外，还存在一个"任务队列"（task queue）。只要异步任务有了运行结果，就在"任务队列"之中放置一个事件。
 1. 一旦"执行栈"中的所有同步任务执行完毕，系统就会读取"任务队列"，看看里面有哪些事件。那些对应的异步任务，于是结束等待状态，进入执行栈，开始执行。
 1. 主线程不断重复上面的第三步。

只要主线程空了，就会去读取"任务队列"，这就是JavaScript的运行机制。这个过程会不断重复。 

"任务队列"是一个事件的队列（也可以理解成消息的队列），IO设备完成一项任务，就在"任务队列"中添加一个事件，表示相关的异步任务可以进入"执行栈"了。主线程读取"任务队列"，就是读取里面有哪些事件。
"任务队列"中的事件，除了IO设备的事件以外，还包括一些用户产生的事件（比如鼠标点击、页面滚动等等），比如$(selectot).click(function)，这些都是相对耗时的操作。只要指定过这些事件的回调函数，这些事件发生时就会进入"任务队列"，等待主线程读取。
所谓"回调函数"（callback），就是那些会被主线程挂起来的代码，前面说的点击事件$(selectot).click(function)中的function就是一个回调函数。异步任务必须指定回调函数，当主线程开始执行异步任务，就是执行对应的回调函数。例如ajax的success，complete，error也都指定了各自的回调函数，这些函数就会加入“任务队列”中，等待执行。


本文思想来源：http://www.cnblogs.com/c3gen/p/6170504.html 

如何实现异步编程请看阮一峰老师的： http://www.ruanyifeng.com/blog/2012/12/asynchronous%EF%BC%BFjavascript.html

#### 10. 写出常见的http状态码及含义

状态码 | 状态码英文名称 | 中文描述
---|---|---
100 | Continue | 继续。客户端应继续其请求
101 | Switching Protocols | 	切换协议。服务器根据客户端的请求切换协议。只能切换到更高级的协议，例如，切换到HTTP的新版本协议
200	 | OK | 请求成功。一般用于GET与POST请求
201	 | Created	 | 已创建。成功请求并创建了新的资源
202	 | Accepted	 | 已接受。已经接受请求，但未处理完成
203	 | Non-Authoritative Information | 	非授权信息。请求成功。但返回的meta信息不在原始的服务器，而是一个副本
204	 | No Content | 无内容。服务器成功处理，但未返回内容。在未更新网页的情况下，可确保浏览器继续显示当前文档
205	| Reset Content	| 重置内容。服务器处理成功，用户终端（例如：浏览器）应重置文档视图。可通过此返回码清除浏览器的表单域
206	| Partial Content | 部分内容。服务器成功处理了部分GET请求
300	| Multiple Choices | 	多种选择。请求的资源可包括多个位置，相应可返回一个资源特征与地址的列表用于用户终端（例如：浏览器）选择
301	| Moved Permanently | 	永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替
302 | Found	| 临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI
303	| See Other	| 查看其它地址。与301类似。使用GET和POST请求查看
304	| Not Modified | 未修改。所请求的资源未修改，服务器返回此状态码时，不会返回任何资源。客户端通常会缓存访问过的资源，通过提供一个头信息指出客户端希望只返回在指定日期之后修改的资源
305	| Use Proxy	| 使用代理。所请求的资源必须通过代理访问
306	| Unused | 已经被废弃的HTTP状态码
307	| Temporary Redirect	| 临时重定向。与302类似。使用GET请求重定向
400	| Bad Request	| 客户端请求的语法错误，服务器无法理解
401	| Unauthorized	| 请求要求用户的身份认证
402	| Payment Required	| 保留，将来使用
403	| Forbidden	| 服务器理解请求客户端的请求，但是拒绝执行此请求
404	| Not Found	| 服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置"您所请求的资源无法找到"的个性页面
405	| Method Not Allowed | 客户端请求中的方法被禁止
406	| Not Acceptable	| 服务器无法根据客户端请求的内容特性完成请求
407	| Proxy Authentication Required | 	请求要求代理的身份认证，与401类似，但请求者应当使用代理进行授权
408	| Request Time-out	| 服务器等待客户端发送的请求时间过长，超时
409	| Conflict	| 服务器完成客户端的PUT请求是可能返回此代码，服务器处理请求时发生了冲突
410	| Gone	| 客户端请求的资源已经不存在。410不同于404，如果资源以前有现在被永久删除了可使用410代码，网站设计人员可通过301代码指定资源的新位置
411	| Length Required	| 服务器无法处理客户端发送的不带Content-Length的请求信息
412	| Precondition Failed	| 客户端请求信息的先决条件错误
413	| Request Entity Too Large | 	由于请求的实体过大，服务器无法处理，因此拒绝请求。为防止客户端的连续请求，服务器可能会关闭连接。如果只是服务器暂时无法处理，则会包含一个Retry-After的响应信息
414	| Request-URI Too Large	| 请求的URI过长（URI通常为网址），服务器无法处理
415	| Unsupported Media Type	| 服务器无法处理请求附带的媒体格式
416	| Requested range not satisfiable	| 客户端请求的范围无效
417	| Expectation Failed	| 服务器无法满足Expect的请求头信息
500	| Internal Server Error	| 服务器内部错误，无法完成请求
501	| Not Implemented	| 服务器不支持请求的功能，无法完成请求
502	| Bad Gateway	| 充当网关或代理的服务器，从远端服务器接收到了一个无效的请求
503	| Service Unavailable | 	由于超载或系统维护，服务器暂时的无法处理客户端的请求。延时的长度可包含在服务器的Retry-After头信息中
504	| Gateway Time-out	| 充当网关或代理的服务器，未及时从远端服务器获取请求
505	| HTTP Version not supported	| 服务器不支持请求的HTTP协议的版本，无法完成处理
