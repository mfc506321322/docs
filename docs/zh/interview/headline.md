---
title: 今日头条
sidebar: auto
sidebarDepth: 2
---
# 今日头条面试总结

## 一、HTML基础题目

#### 行内元素有哪些?块级元素有哪些? 空(void)元素有那些?
> CSS规范规定，每个元素都有display属性，确定该元素的类型，每个元素都有默认的display值，如div的display默认值为“block”，则为“块级”元素；span默认display属性值为“inline”，是“行内”元素。
- 行内元素有：a b span img input select strong（强调的语气）
- 块级元素有：div ul ol li dl dt dd h1 h2 h3 h4…p
- 常见的空元素：\<br>\<hr>\<img>\<input>\<link>\<meta>
鲜为人知的是：\<area><base>\<col>\<command>\<embed>\<keygen>\<param>\<source>\<track>\<wbr>
    
####  页面导入样式时，使用link和@import有什么区别?
- link
    1. link属于XHTML标签，除了加载CSS外，还能用于定义RSS, 定义rel连接属性等作用
    2. 页面被加载的时，link会同时被加载
    3. link是XHTML标签，无兼容问题
- @import
    1. @import是CSS提供的，只能用于加载CSS
    2. @import引用的CSS会等到页面被加载完再加载
    3. import是CSS2.1 提出的，只在IE5以上才能被识别

#### 常见的浏览器内核有哪些?
- Trident内核：IE,MaxThon,TT,The World,360,搜狗浏览器等。[又称MSHTML]
- Gecko内核：Netscape6及以上版本，FF,MozillaSuite/SeaMonkey等
- Presto内核：Opera7及以上。      [Opera内核原为：Presto，现为：Blink;] 
- Webkit内核：Safari,Chrome等。   [ Chrome的：Blink（WebKit的分支）] 

#### HTML5有哪些新特性、移除了那些元素?如何处理HTML5新标签的浏览器兼容问题?
- HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。 
    - 绘画 canvas;
    - 用于媒介回放的 video 和 audio 元素; 
    - 本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失; 
    - sessionStorage 的数据在浏览器关闭后自动删除; 
    - 语意化更好的内容元素，比如 article、footer、header、nav、section;
    - 表单控件，calendar、date、time、email、url、search;
    - 新的技术webworker, websocket, Geolocation;
- 移除的元素：
    - 纯表现的元素：basefont，big，center，font, s，strike，tt，u;
    - 对可用性产生负面影响的元素：frame，frameset，noframes；
 
- 支持HTML5新标签： 
    - E8/IE7/IE6支持通过document.createElement方法产生的标签，
可以利用这一特性让这些浏览器支持HTML5新标签，
浏览器支持新标签后，还需要添加标签默认的样式。
当然也可以直接使用成熟的框架、比如html5shim;

        \<[if lt IE 9]> 
        \<script>src="http://html5shim.googlecode.com/svn/trunk/html5.js">\</script>
    \<[endif]>
* 如何区分HTML5： 
    - DOCTYPE声明\新增的结构元素\功能元素 
    - H5新特性:
        表单 画布 音视频 地理定位 媒体查询 css新特性 离线缓存 本地存储 拖拽 
#### HTML5的离线储存怎么使用，工作原理能不能解释一下?浏览器是怎么对HTML5的离线储存资源进行管理和加载的呢?
> 原理：
    HTML5的离线存储是基于一个新建的.appcache文件的缓存机制(不是存储技术)，通过这个文件上的解析清单离线存储资源，这些资源就会像cookie一样被存储了下来。之后当网络在处于离线状态下时，浏览器会通过被离线存储的数据进行页面展示。
- 如何使用：
    - 页面头部像下面一样加入一个manifest的属性；
在cache.manifest文件的编写离线存储的资源；
    CACHE MANIFEST
    #v0.11
    CACHE:
     js/app.js
     css/style.css
    NETWORK:
    resourse/logo.png
    FALLBACK:
    / /offline.html
    在离线状态时，操作window.applicationCache进行需求实现。
- 如何管理和加载：
    - 在线的情况下，浏览器发现html头部有manifest属性，它会请求manifest文件，如果是第一次访问app，那么浏览器就会根据manifest文件的内容下载相应的资源并且进行离线存储。如果已经访问过app并且资源已经离线存储了，那么浏览器就会使用离线的资源加载页面，然后浏览器会对比新的manifest文件与旧的manifest文件，如果文件没有发生改变，就不做任何操作，如果文件改变了，那么就会重新下载文件中的资源并进行离线存储。
    - 离线的情况下，浏览器就直接使用离线存储的资源。
#### 请描述一下 cookies，sessionStorage 和 localStorage 的区别?
- cookie是网站为了标示用户身份而储存在用户本地终端（Client Side）上的数据（通常经过加密），cookie还可以设置有效时间
cookie数据始终在同源的http请求中携带（即使不需要），记会在浏览器和服务器间来回传递，
每次ajax请求都会吧cookie传送到后台，cookie一半用做用户登陆，后台可以根据cookie信息判断用户是否登陆状态
- 
    sessionStorage和localStorage不会自动把数据发给服务器，仅在本地保存。
- 区别
    1.  存储大小：
        - cookie数据大小不能超过4k。
        - sessionStorage和localStorage 虽然也有存储大小的限制，但比cookie大得多，可以达到5M或更大。 
    2.  有期时间：
        - localStorage 存储持久数据，浏览器关闭后数据不丢失除非主动删除数据； 
        - sessionStorage 数据在当前浏览器窗口关闭后自动删除。 
        - cookie 设置的cookie过期时间之前一直有效，即使窗口或浏览器关闭 
####  如何实现浏览器内多个标签页之间的通信? 
- WebSocket、也可以调用localstorge、cookies等本地存储方式，还可以使用页面的路有参数传递
- localstorge另一个浏览上下文里被添加、修改或删除时，它都会触发一个事件，我们通过监听事件，控制它的值来进行页面信息通信；
#### websocket如何兼容低浏览器?
- Adobe Flash Socket 
- ActiveX HTMLFile (IE)
- 基于 multipart 编码发送 XHR 
- 基于长轮询的 XHR
#### 如何在页面上实现一个圆形的可点击区域?
1. 方法一
    map+area，\<img>通过usemap映射到的circle形。
    ```
    <img src="images/lanlvseImg.png" usemap="#Map" />    
    <map name="Map" id="Map">  
        <area shape="circle" coords="100,100,50" href="http://www.baidu.com" target="_blank"/>  
    </map>
    ```
2. 方法二
    border-radius(H5)
    ```

    <style>  
        .circle{ 
            /* 圆设置 */
            width:100px; 
            height:100px; 
            border-radius: 50%; 
            cursor: pointer; 
            /* 文字设置 */
            position: absolute; 
            left:50px; 
            top:50px; 
            line-height: 100px; 
            text-align: center; 
            color: white; 
            background-color:dimgray; 
        } 
    </style> 

    <div class="circle"></div>
    ```
3. 方法三
    js实现

        获取鼠标点击位置坐标，判断其到圆点的距离是否不大于圆的半径，来判断点击位置是否在圆内。 
        求点在不在圆上的简单算法、获取鼠标坐标等等 
        两点之间的距离计算公式
        |AB|=Math.abs(Math.sqrt(Math.pow(X2-X1),2)+Math.pow(Y2-Y1,2)))
        假设圆心为（100,100）,半径为50，在圆内点击弹出相应的信息，在圆外显示不在圆内的信息
    ```
    document.onclick = function(e) {    
        var r = 50;   
        var x1 = 100;  
        var y1 = 100;  
        var x2= e.clientX;  
        var y2= e.clientY;    
        var distance = Math.abs(Math.sqrt(Math.pow(x2 - x1, 2) + Math.pow(y2 - y1, 2)));    
        if (distance <= 50)  
            alert("Ok!");    
    }   
    ```

## 二、CSS基础题目

#### 网页验证码是干嘛的，是为了解决什么安全问题?
- 验证码是为了防止一些人使用软件恶意注册、发帖等行为而设的。
- 它的存在是为了确保登陆网站的是一个坐在电脑面前的真人，而不是一个自动登陆的软件。
#### 介绍一下标准的CSS的盒子模型?与低版本IE的盒子模型有什么不同的?
- CSS盒子模型：由四个属性组成的外边距(margin)、内边距(padding)、边界(border)、内容区(width和height);
- 标准的CSS盒子模型和低端IE CSS盒子模型不同：宽高不一样
- 标准的css盒子模型宽高就是内容区宽高；
- 低端IE css盒子模型宽高 内边距﹢边界﹢内容区；
#### CSS选择符有哪些?哪些属性可以继承?
- css选择器：
    - 类型选择符（body）、群组选择符（h1，h2，h3，span）、包含选择符（h2 span）、ID选择符（#id）、Class选择符（.content）
- 哪些可以继承：
    - class属性，伪类A标签，列表ul、li、dl、dd、dt可以继承
- 拓展：css优先级
    - !important > 行内样式>ID选择器 > 类选择器 > 标签 > 通配符 > 继承 > 浏览器默认属性
#### 如何居中div?如何居中一个浮动元素?如何让绝对定位的div居中?
>水平垂直居中问题，在css中margin: 0 auto;可以实现水平居中，但是在垂直居中方面一直没有特定的属性，直到css3的出现，有了弹性盒，可以通过设置弹性盒直接设置居中位置，做浏览器兼容的话可以通过使用一些hack处理 负margin方法，table-cell方法，位移方法
 
- 负margin方法：
    ```
    CSS代码
    .container{      
            width: 500px;       
            height: 400px;       
            border: 2px solid #379;       
            position: relative;  
    } 
    .inner{      
            width: 480px;       
            height: 380px;       
            background-color: #746;       
            position: absolute;       
            top: 50%;       
            left: 50%;       
            margin-top: -190px; /*height的一半*/       
            margin-left: -240px; /*width的一半*/  
    }
    HTML代码
    <div class="container">
        <div class="inner"></div>
    </div> 

    这里，我们首先用top:50%和left:50%让inner的坐标原点（左上角）移动到container的中心，然后再利用负margin让它往左偏移自身宽的一半，再往上偏移自身高的一半，这样inner的中心点就跟container的中心点对齐了。
    ```
  
- table－cell方法
    ```
    CSS代码：
    div{    
         width: 300px; 
         height: 300px; 
         border: 3px solid #555; 
         display: table-cell; 
         vertical-align: middle; 
         text-align: center; 
    }
    img{
         vertical-align: middle; 
    }
    HTML代码：
    <div>     <img src="mm.jpg"> </div> 
     
    通过将盒子转换为table元素，table元素本身是可以通过属性来控制位置，div上面的vertical-align: middle是控制垂直方向上的居中的，而text-align: center是控制水平方向的
    ```
- 弹性盒子法
    ```
    CSS代码：
    .container{
           width: 300px; 
           height: 200px; 
           border: 3px solid #546461; 
           display: -webkit-flex; 
           display: flex; 
           -webkit-align-items: center; 
           align-items: center; 
           -webkit-justify-content: center; 
           justify-content: center;  
    } 
    .inner{
           border: 3px solid #458761; 
           padding: 20px;  
    }
    HTML代码：
    <div class="container"> 
         <div class="inner"> 
             我在容器中水平垂直居中 
         </div> 
    </div>

    align-items控制垂直方向的居中，justify-content控制水平方向的居中。这是CSS3的新方法
    ```
- 位移方法
    - 位移方法和margin定位方法一样，只不过吧margin改成了位移不需要计算一半是多少，直接 transform:translate(-50%,--50%) 

#### display有哪些值?说明他们的作用。
> 值包括 none | inline | block | list-item | inline-block | table | inline-table | table-caption | table-cell | table-row | table-row-group | table-column | table-column-group | table-footer-group | table-header-group | run-in | box | inline-box | flexbox | inline-flexbox | flex | inline-flex
默认值：inline

![image](https://image-static.segmentfault.com/338/496/3384967612-5ad70be123d77_articlex)
#### position的值relative和absolute定位原点是?
- relative（相对定位）：定位原点是元素本身所在位置； 
- absolute（绝对定位）：定位原点是离自己这一级元素最近的一级position设置为absolute或者relative的父元素的左上角为原点的 
- static: 默认值。没有定位，元素出现在正常的流中（忽略 top, bottom, left, right z-index 声明）
- inherit  :规定从父元素继承 position 属性的值。 
#### CSS3有哪些新特性?
- css3选择器
- css3边框
- css3背景
- css3渐变
- css3文本效果
- css3字体
- css3转换和变形
- css3过渡
- css3动画
- css3多列
- css3盒模型
- css3弹性盒
- css3多媒体查询
#### 请解释一下CSS3的Flexbox(弹性盒布局模型),以及适用场景?
- Flexbox 可以简便、完整、响应式地实现各种页面布局。
(Flexbox又叫弹性盒模型。它可以简单使用一个元素居中（包括水平垂直居中），可以让扩大和收缩元素来填充容器的可利用空间，可以改变源码顺序独立布局，以及还有其他的一些功能。)
- 用于不同尺寸屏幕中创建可自动扩展和收缩布局,
#### li与li之间有看不见的空白间隔是什么原因引起的？有什么解决办法？
- 行框的排列会受到中间空白（回车\空格）等的影响，因为空格也属于字符,这些空白也会被应用样式，占据空间，所以会有间隔
- li 标签之间的空白，可以通过设置 li 标签的 font-size 为 0，可以解决
#### 经常遇到的浏览器的兼容性有哪些?原因，解决方法是什么，常用hack的技巧 ?
1. 问题：png24位的图片在iE6浏览器上出现背景，
    - 解决：解决方案是做成PNG8.
2. 问题：浏览器默认的margin和padding不同。
    - 解决：方案是加一个全局的*{margin:0;padding:0;}来统一。
3. 问题：IE6双边距bug:块属性标签float后，又有横行的margin情况下，在ie6显示margin比设置的大。
浮动ie产生的双倍距离 #box{ float:left; width:10px; margin:0 0 0 100px;}这种情况之下IE会产生20px的距离，
    - 解决：解决方案是在float的标签样式控制中加入 ——_display:inline;将其转化为行内属性。(_这个符号只有ie6会识别)渐进识别的方式，从总体中逐渐排除局部。
首先，巧妙的使用“\9”这一标记，将IE游览器从所有情况中分离出来。 接着，再次使用“+”将IE8和IE7、IE6分离开来，这样IE8已经独立识别。
    ```
        css 
          .bb{ 
               background-color:#f1ee18;/*所有识别*/ 
              .background-color:#00deff\9; /*IE6、7、8识别*/ 
              +background-color:#a200ff;/*IE6、7识别*/ 
              _background-color:#1e0bd1;/*IE6识别*/ 
          } 
    ```

4. 问题：IE下,可以使用获取常规属性的方法来获取自定义属性,也可以使用getAttribute()获取自定义属性，Firefox下,只能使用getAttribute()获取自定义属性.
    - 解决：解决方法:统一通过getAttribute()获取自定义属性.
5. 问题：IE下,even对象有x,y属性,但是没有pageX,pageY属性，Firefox下,event对象有pageX,pageY属性,但是没有x,y属性
    - 解决：（条件注释）缺点是在IE浏览器下可能会增加额外的HTTP请求数。
6. 问题：Chrome 中文界面下默认会将小于 12px 的文本强制按照 12px 显示, 
    - 解决：可通过加入 CSS 属性 -webkit-text-size-adjust: none; 解决. 
7. 问题：超链接访问过后hover样式就不出现了 被点击访问过的超链接样式不在具有hover和active了
    - 解决：方法是改变CSS属性的排列顺序:L-V-H-A : a:link {} a:visited {} a:hover {} a:active {}
#### absolute的containing block计算方式跟正常流有什么不同?
无论属于哪种，都要先找到其祖先元素中最近的 position 值不为 static 的元素，然后再判断： 
- 若此元素为 inline 元素，则 containing block 为能够包含这个元素生成的第一个和最后一个 inline box 的 padding box (除 margin, border 外的区域) 的最小矩形； 
- 否则,则由这个祖先元素的 padding box 构成。 
如果都找不到，则为 initial containing block。

- 补充：
    1. static(默认的)/relative：简单说就是它的父元素的内容框（即去掉padding的部分）
    2. absolute: 向上找最近的定位为absolute/relative的元素 
    3. fixed: 它的containing block一律为根元素(html/body)，根元素也是initial containing block 
#### CSS里的visibility属性有个collapse属性值是干嘛用的?在不同浏览器下以后什么区别
>当一个元素的visibility属性被设置成collapse值后，对于一般的元素，它的表现跟hidden是一样的。但例外的是，如果这个元素是table相关的元素，例如table行，table group，table列，table column group，它的表现却跟display: none一样，也就是说，它们占用的空间也会释放。
- 在谷歌浏览器里，使用collapse值和使用hidden值没有什么区别。
- 在火狐浏览器、Opera和IE11里，使用collapse值的效果就如它的字面意思：table的行会消失，它的下面一行会补充它的位置。
#### position跟display、margin collapse、overflow、float这些特性相互叠加后会怎么样?
类似于优先级机制：position：absolute/fixed优先级最高，有他们在时，float不起作用，display值需要调整。float 或者absolute定位的元素，只能是块元素或表格。
- display属性规定元素应该生成的框的类型；
- position属性规定元素的定位类型；
- float属性是一种布局方式，定义元素在哪个方向浮动。
#### 请解释一下为什么会出现浮动和什么时候需要清除浮动?清除浮动的方式？
> 浮动元素碰到包含它的边框或者浮动元素的边框停留。由于浮动元素不在文档流中，所以文档流的块框表现得就像浮动框不存在一样。浮动元素会漂浮在文档流的块框上。

- 浮动带来的问题：
    1.父元素的高度无法被撑开，影响与父元素同级的元素
    2.与浮动元素同级的非浮动元素（内联元素）会跟随其后
    3.若非第一个元素浮动，则该元素之前的元素也需要浮动，否则会影响页面显示的结构。
    - 解决方法：
使用CSS中的clear:both;属性来清除元素的浮动可解决2、3问题，对于问题1，添加如下样式，给父元素添加clearfix样式：
.clearfix:after{content: ".";display: block;height: 0;clear: both;visibility: hidden;}
.clearfix{display: inline-block;} /* for IE/Mac */

- 清除浮动的方式：
    1.额外标签法，\<div style="clear:both;"></div>（缺点：不过这个办法会增加额外的标签使HTML结构看起来不够简洁。）
    2.使用after伪类
    ```
        #parent:after{
            content:".";
            height:0;  
            visibility:hidden;
            display:block;
            clear:both; 
        }
    ```
    3.浮动外部元素
    4.设置overflow为hidden或者auto
#### 使用 CSS 预处理器吗?喜欢那个?
- SASS (SASS、LESS没有本质区别，只因为团队前端都是用的SASS)，可以使用sass和less对css做模块化开发，定制样式的组件
#### CSS优化、提高性能的方法有哪些?
- 将样式表放到页面顶部
- 不使用CSS表达式
- 不使用@import
- 不使用IE的Filter
#### 在网页中的应该使用奇数还是偶数的字体?为什么呢?
使用偶数字体。偶数字号相对更容易和 web 设计的其他部分构成比例关系。Windows 自带的点阵宋体（中易宋体）从 Vista 开始只提供 12、14、16 px 这三个大小的点阵，而 13、15、17 px时用的是小一号的点。（即每个字占的空间大了 1 px，但点阵没变），于是略显稀疏。
#### margin和padding分别适合什么场景使用?
- 何时使用margin：
    1.需要在border外侧添加空白
    2.空白处不需要背景色
    3.上下相连的两个盒子之间的空白，需要相互抵消时。
- 何时使用padding：
    1.需要在border内侧添加空白
    2.空白处需要背景颜色
    3.上下相连的两个盒子的空白，希望为两者之和。
    4.兼容性的问题：在IE5 IE6中，为float的盒子指定margin时，左侧的margin可能会变成两倍的宽度。通过改变padding或者指定盒子的display：inline解决。
#### 抽离样式模块怎么写，说出思路，有无实践经验
> webpack中的mini-css-extract-pluginc插件

- 此插件将CSS提取到单独的文件中。它为每个包含CSS的JS文件创建一个CSS文件。它支持CSS和SourceMaps的按需加载。
    它建立在新的webpack v4功能（模块类型）之上，并且需要webpack 4才能工作。
> webpack中extract-text-webpack-plugin插件

-  参考：https://www.npmjs.com/package/mini-css-extract-plugin?tdsourcetag=s_pctim_aiomsg

    ```
        //抽离css样式插件   此插件需要升级 cnpm i --save-dev extract-text-webpack-plugin@next
        const ExtractTextPlugin = require('extract-text-webpack-plugin');
        module.exports = {
            rules: [{
                {
                    test: /\.css$/, //css文件
                    // use: ['style-loader', 'css-loader'] //先加载style-loader
                    use: ExtractTextPlugin.extract({ //抽离样式
                        fallback: 'style-loader',
                        use: 'css-loader'
                    })
                }, {
                    //sass-loader 必须配合node-sass使用
                    test: /\.(sass|scss)$/, //sass,scss文件
                    // use: ['style-loader', 'css-loader', 'sass-loader']
                    //抽离样式
                    use: ExtractTextPlugin.extract({
                        fallback: 'style-loader',
                        //style-loader是css没有被提取 需要把loader输出的内容(style标签)返回 
                        use: [{
                                //css-loader将sass转换成css文件并且import导出模块
                                loader: 'css-loader',
                                options: { //配置项
                                    minimize: true //是否压缩 true压缩为min文件 false不压缩
                                }
                            }, 'sass-loader' //sass-loader解析css-loader  
                        ]
                    })
                }
            }],
            plugins: [
                new ExtractTextPlugin(''), //最终在出口文件的默认创建的文件中生成的css文件名
            ]
        }
    ```
#### 元素竖向的百分比设定是相对于容器的高度吗?
> 不是，是相对于容器宽度。

当按百分比设定一个元素的宽度时，它是相对于父容器的宽度计算的，但是，对于一些表示竖向距离的属性，例如 padding-top , padding-bottom , margin-top , margin-bottom 等，当按百分比设定它们时，依据的也是父容器的宽度，而不是高度。
#### 全屏滚动的原理是什么?用到了CSS的那些属性？
> 原理：有点类似于轮播，整体的元素一直排列下去，假设有5个需要展示的全屏页面，那么高度是500%，只是展示100%，剩下的可以通过transform进行y轴定位，也可以通过margin-top实现

用到了overflow：hidden；transition：all 1000ms ease；
#### 什么是响应式设计?响应式设计的基本原理是什么?如何兼容低版本的IE?
响应式网站设计(Responsive Web design)是一个网站能够兼容多个终端，而不是为每一个终端做一个特定的版本。
基本原理是通过媒体查询检测不同的设备屏幕尺寸做处理。
页面头部必须有meta声明的viewport。
```
    <meta name=’viewport’ content=”width=device-width, initial-scale=1. maximum-scale=1,user-scalable=no”>
```
#### 视差滚动效果，如何给每页做不同的动画?(回到顶部，向下滑动要再次出现，和只出现一次分别怎么做?)
> 原理：视差滚动（Parallax Scrolling）就是这样的效果之一。这种技术通过在网页向下滚动的时候，控制背景的移动速度比前景的移动速度慢来创建出令人惊叹的3D效果。
- （1）CSS3实现
    - 优点：开发时间短、性能和开发效率比较好，缺点是不能兼容到低版本的浏览器
- （2）jquery实现
    通过控制不同层滚动速度，计算每一层的时间，控制滚动效果。
    - 优点：能兼容到各个版本的，效果可控性好
    - 缺点：开发起来对制作者要求高
- （3）插件实现方式
例如：parallax-scrolling，兼容性十分好
#### ::before 和 :after中双冒号和单冒号 有什么区别?解释一下这2个伪元素的作用。
- 单冒号(:)用于CSS3伪类，双冒号(::)用于CSS3伪元素。
- ::before就是以一个子元素的存在，定义在元素主体内容之前的一个伪元素。并不存在于dom之中，只存在在页面之中。
- :before 和 :after 这两个伪元素，是在CSS2.1里新出现的。起初，伪元素的前缀使用的是单冒号语法，但随着Web的进化，在CSS3的规范里，伪元素的语法被修改成使用双冒号，成为::before ::after
#### 你对line-height是如何理解的?
> 行高是指一行文字的高度，具体说是两行文字间基线的距离。CSS中起高度作用的是height和line-height，没有定义height属性，最终其表现作用一定是line-height。
- 单行文本垂直居中：把line-height值设置为height一样大小的值可以实现单行文字的垂直居中，其实也可以把height删除。
- 多行文本垂直居中：需要设置display属性为inline-block。
#### 设置元素浮动后，该元素的display值是多少?
- 自动变成了 display:block
用 window.getComputedStyle(element).display 看了一下确实是 block
#### 让页面里的字体变清晰，变细用CSS怎么做?
- -webkit-font-smoothing: antialiased;
#### font-style属性可以让它赋值为“oblique” oblique是什么意思?
- 倾斜的字体样式
与italic的区别：italic和oblique都是向右倾斜的文字, 但区别在于Italic是指斜体字，而Oblique是倾斜的文字，对于没有斜体的字体应该使用Oblique属性值来实现倾斜的文字效果。也就是说：Italic是使用文字的斜体，Oblique是让没有斜体属性的文字倾斜。
#### position:fixed;在android下无效怎么处理?
```
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no"/>
```
#### 如果需要手动写动画，你认为最小时间间隔是多久，为什么?
多数显示器默认频率是60Hz，即1秒刷新60次，所以理论上最小间隔为1/60*1000ms ＝ 16.7ms
#### display:inline-block 什么时候会显示间隙?
- 有空格时候会有间隙。 解决：移除空格
- margin正值的时候。 解决：margin使用负值
#### overflow: scroll时不能平滑滚动的问题怎么处理?
- 答案一：
-webkit-overflow-scrolling: touch;
- 答案二：
（1）高度尺寸不确定的时候，使用：overflow-y：scroll;
（2）高度尺寸确定的，要么没有滚动条，要么直接出现，不会出现跳动。
（3）css3计算calc和vw单位巧妙实现滚动条出现页面不跳动：

        .wrap-outer {
            margin-left: calc(100vw - 100%);
        }
        或
        .wrap-outer {
            padding-left: calc(100vw - 100%);
        }
        首先，.wrap-outer指的是居中定宽主体的父级，如果没有，创建一个
        然后，calc是css3的计算
        100vw是浏览器的内部宽度，而100%是可用宽度，不含滚动条
        calc（100vw-100%）是浏览器的滚动条的宽度

#### 有一个高度自适应的div，里面有两个div，一个高度100px，希望另一个填满剩下的高度。
（1）height：calc（100%-100px）
（2）absolute positioning：外层position：relative；
百分百自适应元素 position: absolute; top: 100px; bottom: 0; left: 0
（3）flex 父元素display:flex; flex-direction: column; 下面的子元素的设置flex: 1;
#### png、jpg、gif 这些图片格式解释一下，分别什么时候用。有没有了解过webp?

    （1）png是便携式网络图片（Portable Network Graphics）是一种无损数据压缩位图文件格式， 
    优点是：压缩比高，色彩好。 大多数地方都可以用。可以设置透明背景。
    （2）jpg是一种针对相片使用的一种失真压缩方法，是一种破坏性的压缩，在色调及颜色平滑变化做的 不错。在www上，被用来储存和传输照片的格式。不能设置透明背景。但同等效果下图片大小最小。
    （3）gif是一种位图文件格式，以8位色重现真色彩的图像。可以实现动画效果时候

- webp格式 :
是谷歌在2010年推出的图片格式，压缩率只有jpg的2/3，大小比png小了45%，缺点是压缩的时间更久了 。兼容性不好，目前谷歌和opera支持。
#### 什么是Cookie 隔离?(或者说：请求资源的时候不要让它带cookie怎么做)

    如果静态文件都放在主域名下，那静态文件请求的时候都是带着cookie数据提交给server的，非常浪费流量，所以不如隔离开。

    因为cookie有域的限制，因此不能跨域提交请求，故使用非主要域名的时候，请求头中就不会带有cookie数据，这样可以降低请求头的大小，降低请求时间，从而达到降低整体请求延时的目的。

    同时这种方式不会将cookie传入Web Server，也减少了Web Server对cookie的处理分析环节，提高了webserver的http请求的解析速度。
#### style标签写在body后与body前有什么区别?
- 写在head标签中利于浏览器逐步渲染（resources downloading->CSSOM+DOM->RenderTree(composite)->Layout->paint）。具体渲染过程请参考
http://blog.csdn.net/wozaixia...
- 写在body标签后由于浏览器以逐行方式对html文档进行解析，当解析到写在尾部的样式表（外联或写在style标签）会导致浏览器停止之前的渲染，等待加载且解析样式表完成之后重新渲染，在windows的IE下可能会出现FOUC现象（即样式失效导致的页面闪烁问题）

## 三、JS基础题目

#### 介绍JavaScript的基本数据类型
- Undefined、Null、Boolean、Number、String
#### 说说写JavaScript的基本规范

- 不要在同一行声明多个变量
- 请使用===/!==来比较true/false或者数值
- 使用对象字面量替代new Array这种形式
- 不要使用全局函数
- Switch语句必须带有default分支
- If语句必须使用大括号
- for-in循环中的变量 应该使用var关键字明确限定作用域，从而避免作用域污
#### JavaScript原型，原型链 ? 有什么特点?
- 每个对象都会在其内部初始化一个属性，就是prototype(原型)，当我们访问一个对象的属性时
- 如果这个对象内部不存在这个属性，那么他就会去prototype里找这个属性，这个prototype又会有自己的prototype，于是就这样一直找下去，也就是我们平时所说的原型链的概念
- 关系：instance.constructor.prototype = instance.\_\_proto\_\_
- 特点：
    - JavaScript对象是通过引用来传递的，我们创建的每个新对象实体中并没有一份属于自己的原型副本。当我们修改原型时，与之相关的对象也会继承这一改变
- 当我们需要一个属性的时，Javascript引擎会先看当前对象中是否有这个属性， 如果没有的
就会查找他的Prototype对象是否有这个属性，如此递推下去，一直检索到 Object 内建对象
#### JavaScript有几种类型的值?(堆：原始数据类型和 栈：引用数据类型)，你能画一下他们的内存图吗?
- 栈：原始数据类型（Undefined，Null，Boolean，Number、String）
- 堆：引用数据类型（对象、数组和函数）
- 两种类型的区别是：存储位置不同；
- 原始数据类型直接存储在栈(stack)中的简单数据段，占据空间小、大小固定，属于被频繁使用- 数据，所以放入栈中存储；
- 引用数据类型存储在堆(heap)中的对象,占据空间大、大小不固定,如果存储在栈中，将会影响- 程序运行的性能；引用数据类型在栈中存储了指针，该指针指向堆中该实体的起始地址。当解释- 器寻找引用值时，会首先检索其
- 在栈中的地址，取得地址后从堆中获得实体
    - ![](https://upload-images.jianshu.io/upload_images/5815514-ea451b7431ddfaba?imageMogr2/auto-orient/)
#### Javascript如何实现继承?
- 构造继承
- 原型继承
- 实例继承
- 拷贝继承
- 原型prototype机制或apply和call方法去实现较简单，建议使用构造函数与原型混合方式
```
    function Parent(){
        this.name = 'wang';
    }

    function Child(){
        this.age = 28;
    }
    Child.prototype = new Parent();//继承了Parent，通过原型

    var demo = new Child();
    alert(demo.age);
    alert(demo.name);//得到被继承的属性
    }
```
#### Javascript创建对象的几种方式?
> javascript创建对象简单的说,无非就是使用内置对象或各种自定义对象，当然还可以用JSON；但写法有很多种，也能混合使用
- 对象字面量的方法
```
person={firstname:"Mark",lastname:"Yun",age:25,eyecolor:"black"};
```
- 用function来模拟无参的构造函数
```
 function Person(){}
    var person=new Person();//定义一个function，
              //如果使用new"实例化",该function可以看作是一个Class
        person.name="Mark";
        person.age="25";
        person.work=function(){
        alert(person.name+" hello...");
    }
person.work();
```
- 用function来模拟参构造函数来实现（用this关键字定义构造的上下文属性）
```
function Pet(name,age,hobby){
       this.name=name;//this作用域：当前对象
       this.age=age;
       this.hobby=hobby;
       this.eat=function(){
          alert("我叫"+this.name+",我喜欢"+this.hobby+",
                是个程序员");
       }
    }
    var maidou =new Pet("麦兜",25,"coding");//实例化、创建对象
    maidou.eat();//调用eat方法
```
- 用工厂方式来创建（内置对象）
```
var wcDog =new Object();
     wcDog.name="旺财";
     wcDog.age=3;
     wcDog.work=function(){
       alert("我是"+wcDog.name+",汪汪汪......");
     }
     wcDog.work();
```
- 用原型方式来创建
```
function Dog(){

     }
     Dog.prototype.name="旺财";
     Dog.prototype.eat=function(){
     alert(this.name+"是个吃货");
     }
     var wangcai =new Dog();
     wangcai.eat();
```
- 用混合方式来创建
```
function Car(name,price){
    this.name=name;
    this.price=price; 
}
Car.prototype.sell=function(){
    alert("我是"+this.name+"，我现在卖"+this.price+"万元");
}
    var camry =new Car("凯美瑞",27);
    camry.sell();
```
#### Javascript作用链域?
> 首先在js中有作用域的概念，值得就是一个变量的活动范围，分为全局作用域和局部作用域，全局作用域指的是window，局部作用域指的是每一个函数内部，在作用域中查找一个变量首先在自己当前作用域查找找不到向上级查找，逐层向上找到window为止，找不到就会抛出一个错误，这个查找的过程就叫作用域链，作用域链的作用是保证执行环境里有权访问的变量和函数是有序的，作用域链的变量只能向上访问，变量访问到window对象即被终止，作用域链向下访问变量是不被允许的。作用域链有一个需要要注意的问题就是变量提升，当一个变量的使用在定义之前的时候就会得到一个undefined值，在es6中则不会出现这个问题，es6不允许在定义之前使用
#### 谈谈this对象的理解。
- this总是指向函数的直接调用者（而非间接调用者）
- 在function中this指的的是window
- 如果是实用new 调用的话this指的是当前的实例化对象
- 在事件调用函数中this指的调用事件的window特殊的是在IE中的attachEvent中的this总是指向全局对象Window
- 在定时器中this指的是window，
- 在es6中有一个箭头函数，在箭头函数中this永远指向的是父级对象
#### 什么是window对象? 什么是document对象?
- window:它是一个顶层对象,而不是另一个对象的属性，即浏览器的窗口。
- document:代表整个HTML 文档,可用来访问页面中的所有元素
- Window 对象表示当前浏览器的窗口，是JavaScript的顶级对象。我们创建的所有对象、函数、变量都是 Window 对象的成员。
- Window 对象的方法和属性是在全局范围内有效的。
- Document 对象是 HTML 文档的根节点与所有其他节点（元素节点，文本节点，属性节点, 注释节点）
- Document 对象使我们可以通过脚本对 HTML 页面中的所有元素进行访问
- Document 对象是 Window 对象的一部分，可通过 window.document 属性对其进行访问
#### null，undefined的区别?
- null        表示一个对象被定义了，值为“空值”； 
- undefined   表示不存在这个值。 

   
- typeof undefined               //"undefined" 
    - undefined :是一个表示"无"的原始值或者说表示"缺少值"，就是此处应该有一个值，但是还没有定义。当尝试读取时会返回 undefined； 
例如变量被声明了，但没有赋值时，就等于undefined

- typeof null       		 //"object" 
    - null : 是一个对象(空对象, 没有任何属性和方法)； 
例如作为函数的参数，表示该函数的参数不是对象；
- 注意：
    - 在验证null时，一定要使用　=== ，因为 == 无法分别 null 和　undefined 
    undefined表示"缺少值"，就是此处应该有一个值，但是还没有定义。典型用法是：
    1）变量被声明了，但没有赋值时，就等于undefined。
    2）调用函数时，应该提供的参数没有提供，该参数等于undefined。 
    3）对象没有赋值的属性，该属性的值为undefined。
    4）函数没有返回值时，默认返回undefined。

    - null表示"没有对象"，即该处不应该有值。典型用法是：
    1） 作为函数的参数，表示该函数的参数不是对象。
    2） 作为对象原型链的终点。
#### 写一个通用的事件侦听器函数
```
// event(事件)工具集，来源：github.com/markyun
    markyun.Event = {

        // 视能力分别使用dom0||dom2||IE方式 来绑定事件
        // 参数： 操作的元素,事件名称 ,事件处理程序
        addEvent : function(element, type, handler) {
            if (element.addEventListener) {
                //事件类型、需要执行的函数、是否捕捉
                element.addEventListener(type, handler, false);
            } else if (element.attachEvent) {
                element.attachEvent('on' + type, function() {
                    handler.call(element);
                });
            } else {
                element['on' + type] = handler;
            }
        },
        // 移除事件
        removeEvent : function(element, type, handler) {
            if (element.removeEventListener) {
                element.removeEventListener(type, handler, false);
            } else if (element.datachEvent) {
                element.detachEvent('on' + type, handler);
            } else {
                element['on' + type] = null;
            }
        },
        // 阻止事件 (主要是事件冒泡，因为IE不支持事件捕获)
        stopPropagation : function(ev) {
            if (ev.stopPropagation) {
                ev.stopPropagation();
            } else {
                ev.cancelBubble = true;
            }
        },
        // 取消事件的默认行为
        preventDefault : function(event) {
            if (event.preventDefault) {
                event.preventDefault();
            } else {
                event.returnValue = false;
            }
        },
        // 获取事件目标
        getTarget : function(event) {
            return event.target || event.srcElement;
        }
    }
```
#### [“1”, “2”, “3”].map(parseInt) 答案是多少?
- [1, NaN, NaN]因为 parseInt 需要两个参数 (val, radix)，其中radix 表示解析时用的基数。
- map传了 3个(element, index, array)，对应的 radix 不合法导致解析失败。
#### 关于事件，IE与火狐的事件机制有什么区别? 如何阻止冒泡?
1. 我们在网页中的某个操作（有的操作对应多个事件）。例如：当我们点击一个按钮就会产生一个事件。是可以被 JavaScript 侦测到的行为。 
2. 事件处理机制：IE是事件冒泡、Firefox同时支持两种事件模型，也就是：捕获型事件和冒泡型事件； 
3. ev.stopPropagation();（旧ie的方法 ev.cancelBubble = true;） 
#### 什么是闭包(closure)，为什么要用它?
> 闭包是指有权访问另一个函数作用域中变量的函数，创建闭包的最常见的方式就是在一个函数内创建另一个函数，通过另一个函数访问这个函数的局部变量,利用闭包可以突破作用链域，将函数内部的变量和方法传递到外部。
- 闭包的特性：
1，函数内再嵌套函数
2，内部函数可以引用外层的参数和变量
3，参数和变量不会被垃圾回收机制回收
- 闭包的使用场景
常见的闭包的使用场景就是模块化，用来做模块内部的实现通过接口的扩展贡其他模块使用
在就是闭包可以用来缓存值，减少不必要的技术，例如vue里面的计算属性
#### javascript 代码中的”use strict”;是什么意思 ? 使用它区别是什么?
> use strict是一种ECMAscript 5 添加的（严格）运行模式,这种模式使得 Javascript 在更严格的条件下运行, 
- 使JS编码更加规范化的模式,消除Javascript语法的一些不合理、不严谨之处，减少一些怪异行为。
- 默认支持的糟糕特性都会被禁用，比如不能用with，也不能在意外的情况下给全局变量赋值;
- 全局变量的显示声明,函数必须声明在顶层，不允许在非函数代码块内声明函数,arguments.callee也不允许使用；
- 消除代码运行的一些不安全之处，保证代码运行的安全,限制函数中的arguments修改，严格模式下的eval函数的行为和非严格模式的也不相同;
- 提高编译器效率，增加运行速度；
- 为未来新版本的Javascript标准化做铺垫。
#### 如何判断一个对象是否属于某个类?
- 使用instanceof
if(a instanceof Person){ alert('yes’); }
#### new操作符具体干了什么呢?
- 创建一个空对象，并且 this 变量引用该对象，同时还继承了该函数的原型
- 属性和方法被加入到 this 引用的对象中
- 新创建的对象由 this 所引用，并且最后隐式的返回 this
#### Javascript中，有一个函数，执行时对象查找时，永远不会去查找原型，这个函数是?
- hasOwnProperty
 javaScript中hasOwnProperty函数方法是返回一个布尔值，指出一个对象是否具有指定名称的属性。此方法无法检查该对象的原型链中是否具有该属性；该属性必须是对象本身的一个成员。
- 使用方法：
object.hasOwnProperty(proName)
其中参数object是必选项。一个对象的实例。
proName是必选项。一个属性名称的字符串值。
- 如果 object 具有指定名称的属性，那么JavaScript中hasOwnProperty函数方法返回 true，反之则返回 false。 
#### 能解释下面这段代码的意思吗?
```
[].forEach.call($$("*"),function(a){ a.style.outline="1px solid #"+(~~(Math.random()*(1<<24))).toString(16) }) 
```
- 标签：.net   --   outline   document   参考   foreach   each   call()   tor   
- [].forEach.call()--调用引用数组的forEach方法
- $$("")--等价于document.querySelectortAll("*")
- ~~a--等价于parseInt(a)
- 1<<24--对二进数1小数点右移24位
可参考：https://my.oschina.net/l3ve/blog/330358
#### JS延迟加载的方式有哪些?
- defer和async、动态创建DOM方式（用得最多）、按需异步载入js
#### Ajax 是什么? 如何创建一个Ajax?
> ajax的全称：Asynchronous Javascript And XML。异步传输+js+xml。
- 所谓异步，在这里简单地解释就是：向服务器发送请求的时候，我们不必等待结果，而是可以同时做其他的事情，等到有了结果它自己会根据设定进行后续操作，与此同时，页面是不会发生整页刷新的，提高了用户体验
(1)创建XMLHttpRequest对象,也就是创建一个异步调用对象 
(2)创建一个新的HTTP请求,并指定该HTTP请求的方法、URL及验证信息 
(3)设置响应HTTP请求状态变化的函数 
(4)发送HTTP请求 
(5)获取异步调用返回的数据 
(6)使用JavaScript和DOM实现局部刷新 
         ajax是一种创建交互式网页的计算 
#### 如何解决跨域问题?
> 首先了解下浏览器的同源策略 同源策略/SOP（Same origin policy）是一种约定，由Netscape公司1995年引入浏览器，它是浏览器最核心也最基本的安全功能，如果缺少了同源策略，浏览器很容易受到XSS、CSFR等攻击。所谓同源是指"协议+域名+端口"三者相同，即便两个不同的域名指向同一个ip地址，也非同源

> jsonp、 iframe、window.name、window.postMessage、服务器上设置代理页面 
- 通过jsonp跨域
```
var script = document.createElement('script');
script.type = 'text/javascript';

// 传参并指定回调执行函数为onBack
script.src = 'http://www.....:8080/login?user=admin&callback=onBack';
document.head.appendChild(script);

// 回调执行函数
function onBack(res) {
    alert(JSON.stringify(res));
}
```
- document.domain + iframe跨域
此方案仅限主域相同，子域不同的跨域应用场景
1.）父窗口：(http://www.domain.com/a.html)
    ```
    <iframe id="iframe" src="http://child.domain.com/b.html"></iframe>
    <script>
        document.domain = 'domain.com';
        var user = 'admin';
    </script>
    ```
    2.）子窗口：(http://child.domain.com/b.html)
document.domain = 'domain.com';
// 获取父窗口中变量
alert('get js data from parent ---> ' + window.parent.user);
- nginx代理跨域
- nodejs中间件代理跨域
- 后端在头部信息里面设置安全域名
#### 页面编码和被请求的资源编码如果不一致如何处理?
- 后端响应头设置 charset
- 前端页面\<meta>设置 charset
#### 谈一谈你对ECMAScript6的了解?
- 新增模板字符串（为JavaScript提供了简单的字符串插值功能）
- 箭头函数
- for-of（用来遍历数据—例如数组中的值。）
- arguments对象可被不定参数和默认参数完美代替。
- ES6将promise对象纳入规范，提供了原生的Promise对象。
- 增加了let和const命令，用来声明变量。
- 增加了块级作用域。
- let命令实际上就增加了块级作用域。
- 还有就是引入module模块的概念
#### ECMAScript6 怎么写class么，为什么会出现class这种东西?
- ES6 语法糖 class -- 用 new 关键字 生成实例对象
    ```     
    class Dog{
        constructor(name){
            this.name = name;            
        }
        saySomething(){
            console.log('汪汪汪');      
        }
    }
    var dog = new Dog('LiLy'); //也是通过new实例化
    dog.name //LiLy
    dog.saySomething() //汪汪汪
    ```
    ```
    typeof Dog // "function" 
    Dog.prototype.saySomething(); //汪汪汪
    Dog.prototype.constructor === Dog //ture
    ```
- 表明class其实跟构造函数的实现没有什么本质的差别，类本身也是一个函数，类的所有方法也是定义在prototype上，类本身指向它的构造函数，class的实现还是基于prototype的，它只是把prototype藏起来了。
- 与面向对象语言中类不同的是，ES6的class中只有实例属性，无法定义类成员属性，只能定义方法。
- 语法更加地简洁，不再需要每次都引用prototype去定义类的方法，也方便了编辑器检查代码语法。
#### 异步加载的方式有哪些?
> 异步加载又被称为非阻塞加载，浏览器在下载JS的同时，还会进行后续页面处理。
- 方法一：Script Dom Element
```
(function(){
    var scriptEle = document.createElement("script");
    scriptEle.type = "text/javasctipt";
    scriptEle.async = true;
    scriptEle.src = "http://cdn.bootcss.com/jquery/3.0.0-beta1/jquery.min.js";
    var x = document.getElementsByTagName("head")[0];
    x.insertBefore(scriptEle, x.firstChild);		
 })();
 ```
\<async>属性是HTML5中新增的异步支持。此方法被称为Script DOM Element方法
```
(function(){;
    var ga = document.createElement('script'); 
    ga.type = 'text/javascript'; 
    ga.async = true; 
    ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js'; 
    var s = document.getElementsByTagName('script')[0]; 
    s.parentNode.insertBefore(ga, s); 
})();
```
但是这种加载方式执行完之前会阻止onload事件的触发，而现在很多页面的代码都在onload时还执行额外的渲染工作，所以还是会阻塞部分页面的初始化处理。
- 方法二：onload时的异步加载
```
(function(){
	if(window.attachEvent){
    	window.attachEvent("load", asyncLoad);
    }else{
    	window.addEventListener("load", asyncLoad);
    }
    var asyncLoad = function(){
    	var ga = document.createElement('script'); 
        ga.type = 'text/javascript'; 
        ga.async = true; 
        ga.src = ('https:' == document.location.protocol ? 'https://ssl' : 'http://www') + '.google-analytics.com/ga.js'; 
        var s = document.getElementsByTagName('script')[0]; 
        s.parentNode.insertBefore(ga, s);
    }
})();
```
这种方法只是把插入script的方法放在一个函数里面，然后放在window的onload方法里面执行，这样就解决了阻塞onload事件触发的问题。

注:DOMContentLoaded与load的区别。前者是在document已经解析完成，页面中的dom元素可用，但是页面中的图片，视频，音频等资源未加载完，作用同jQuery中的ready事件；后者的区别在于页面所有资源全部加载完毕。
- 方法三：$(document).ready()
    - 需要引入jquery
    - 兼容所有浏览器
```
$(document).ready(function() {
    alert("加载完成！");
});
```
- 方法四：\<script>标签的async="async"属性
    - async属性是HTML5新增属性，需要Chrome、FireFox、IE9+浏览器支持
    - async属性规定一旦脚本可用，则会异步执行
    - async属性仅适用于外部脚本
    - 此方法不能保证脚本按顺序执行
    - 他们将在onload事件之前完成
```
<script type="text/javascript" src="xxx.js" async="async"></script>
```
- 方法五：\<script>标签的defer="defer"属性
    - defer属性规定是否对脚本执行进行延迟，直到页面加载为止
    - 如果脚本不会改变文档的内容，可将defer属性加入到\<script>标签中，以便加快处理文档的速度
    - 兼容所有浏览器
    - 此方法可以确保所有设置了defer属性的脚本按顺序执行
```
<script type="text/javascript" defer></script>
```
#### DOM操作——怎样添加、移除、移动、复制、创建和查找节点?
- （1）创建新节点
      createDocumentFragment()    //创建一个DOM片段
      createElement()   //创建一个具体的元素
      createTextNode()   //创建一个文本节点
- （2）添加、移除、替换、插入
      appendChild()
      removeChild()
      replaceChild()
      insertBefore() //在已有的子节点前插入一个新的子节点
- （3）查找
      getElementsByTagName()    //通过标签名称
      getElementsByName()    //通过元素的Name属性的值(IE容错能力较强，会得到一个数组，其中包括id等于name值的)
      getElementById()    //通过元素Id，唯一性
#### .call() 和 .apply() 的含义和区别?
- .apply()只有两个参数，第一个参数是调用当前函数的对象，第二个参数是一个数组，里面的值是传入当前调用的函数的参数。
- .cal()可以有多个参数，第一个参数还是调用当前函数的对象，而要传入当前调用的函数的参数是直接用第2、3、4...个参数传入的。

例子中用 add 来替换 sub，add.call(sub,3,1) == add(3,1) ，所以运行结果为：alert(4);

注意：js 中的函数其实是对象，函数名是对 Function 对象的引用。
```
function add(a,b){
    alert(a+b);
}
function sub(a,b){
    alert(a-b);
}
add.call(sub,3,1);
```
#### 数组和对象有哪些原生方法，列举一下?
- 对象Object: create, toString，valueOf，hasOwnProperty
- 数组Array: isArray, splice，forEach，find，concat，pop，push，reverse，shift，slice
参考(https://www.jb51.net/article/34711.htm)
#### JS 怎么实现一个类。怎么实例化这个类
- 构造函数法（this + prototype） -- 用 new 关键字 生成实例对象
    - 缺点：用到了 this 和 prototype，编写复杂，可读性差
    ```
    function Mobile(name, price){
        this.name = name;
        this.price = price;
    }
    Mobile.prototype.sell = function(){
        alert(this.name + "，售价 $" + this.price);
    }
    var iPhone7 = new Mobile("iPhone7", 1000);
    iPhone7.sell();
    ```
- Object.create 法 -- 用 Object.create() 生成实例对象
    - 缺点：不能实现私有属性和私有方法，实例对象之间也不能共享数据
    ```
    var Person = {
        firstname: "Mark",
        lastname: "Yun",
        age: 25,
        introduce: function(){
            alert('I am ' + Person.firstname + ' ' + Person.lastname);
        }
    };

    var person = Object.create(Person);
    person.introduce();

    // Object.create 要求 IE9+，低版本浏览器可以自行部署：
    if (!Object.create) {
    　   Object.create = function (o) {
    　　　 function F() {}
    　　　 F.prototype = o;
    　　　 return new F();
    　　};
    　}
    ```
- 极简主义法（消除 this 和 prototype） -- 调用 createNew() 得到实例对象
    - 优点：容易理解，结构清晰优雅，符合传统的"面向对象编程"的构造
    ``` 
        var Cat = {
            age: 3, // 共享数据 -- 定义在类对象内，createNew() 外
            createNew: function () {
                var cat = {};
                // var cat = Animal.createNew(); // 继承 Animal 类
                cat.name = "小咪";
                var sound = "喵喵喵"; // 私有属性--定义在 createNew() 内，输出对象外
                cat.makeSound = function () {
                alert(sound);  // 暴露私有属性
                };
                cat.changeAge = function(num){
                Cat.age = num; // 修改共享数据
                };
                return cat; // 输出对象
            }
        };

        var cat = Cat.createNew();
        cat.makeSound();
    ```
- ES6 语法糖 class -- 用 new 关键字 生成实例对象
```
    class Point {
       constructor(x, y) {
         this.x = x;
         this.y = y;
       }
       toString() {
         return '(' + this.x + ', ' + this.y + ')';
       }
    }
    var point = new Point(2, 3);
```
#### JavaScript中的作用域与变量声明提升?
- JavaScript 作用域：
    - 在 Java、C 等语言中，作用域为 for 语句、if 语句或{}内的一块区域，称为作用域；
    - 而在 JavaScript 中，作用域为 function(){}内的区域，称为函数作用域。
- JavaScript 变量声明提升：
    - 在 JavaScript 中，函数声明与变量声明经常被 JavaScript 引擎隐式地提升到当前作用域的顶部。
    - 声明语句中的赋值部分并不会被提升，只有名称被提升
    -  函数声明的优先级高于变量，如果变量名跟函数名相同且未赋值，则函数声明会覆盖变量声明
    - 如果函数有多个同名参数，那么最后一个参数（即使没有定义）会覆盖前面的同名参数
#### 如何编写高性能的Javascript?
- 遵循严格模式："use strict";
- 将 js 脚本放在页面底部，加快渲染页面
- 将 js 脚本将脚本成组打包，减少请求
- 使用非阻塞方式下载 js 脚本
- 尽量使用局部变量来保存全局变量
- 尽量减少使用闭包
- 使用 window 对象属性方法时，省略 window
- 尽量减少对象成员嵌套
- 缓存 DOM 节点的访问
- 通过避免使用 eval() 和 Function() 构造器
- 给 setTimeout() 和 setInterval() 传递函数而不是字符串作为参数
- 尽量使用直接量创建对象和数组
- 最小化重绘(repaint)和回流(reflow)
#### 那些操作会造成内存泄漏?
- 内存泄漏指任何对象在您不再拥有或需要它之后仍然存在
- 垃圾回收器定期扫描对象，并计算引用了每个对象的其他对象的数量。如果一个对象的引用数- 量为 0（没有其他对象引用过该对象），或对该对象的惟一引用是循环的，那么该对象的内存- 即可回收
- setTimeout 的第一个参数使用字符串而非函数的话，会引发内存泄漏
- 闭包、控制台日志、循环（在两个对象彼此引用且彼此保留时，就会产生一个循环）

## 四、jQuery基础题目

#### jQuery.fn的init方法返回的this指的是什么对象?为什么要返回this?
- jQuery.fn 的 init 方法 返回的 this 就是 jQuery 对象
- 用户使用 jQuery() 或 $() 即可初始化 jQuery 对象，不需要动态的去调用 init 方法
#### jQuery 的属性拷贝(extend)的实现原理是什么，如何实现深拷贝?
- 浅拷贝（只复制一份原始对象的引用）
var newObject = $.extend({}, oldObject);
- 深拷贝（对原始对象属性所引用的对象进行进行递归拷贝）
var newObject = $.extend(true, {}, oldObject);
#### jquery.extend 与 jquery.fn.extend的区别?
- jquery.extend 为jquery类添加类方法，可以理解为添加静态方法
- jquery.fn.extend:
源码中jquery.fn = jquery.prototype，所以对jquery.fn的扩展，就是为jquery类添加成员函数

使用：

    jquery.extend扩展，需要通过jquery类来调用，而jquery.fn.extend扩展，所有jquery实例都可以直接调用。
- $.fn.extend() 和 $.extend() 是 jQuery 为扩展插件提拱了两个方法
- $.extend(object); // 为jQuery添加“静态方法”（工具方法）
```
$.extend({
　　min: function(a, b) { return a < b ? a : b; },
　　max: function(a, b) { return a > b ? a : b; }
});
$.min(2,3); //  2
$.max(4,5); //  5
```
- $.extend([true,] targetObject, object1[, object2]); // 对targt对象进行扩展
```
var settings = {validate:false, limit:5};
var options = {validate:true, name:"bar"};
$.extend(settings, options);  // 注意：不支持第一个参数传 false
// settings == {validate:true, limit:5, name:"bar"}
```
- $.fn.extend(json); // 为jQuery添加“成员函数”（实例方法）
```
$.fn.extend({
   alertValue: function() {
      $(this).click(function(){
        alert($(this).val());
      });
   }
});

$("#email").alertValue();
```
#### jQuery 的队列是如何实现的?队列可以用在哪些地方?
- jQuery 核心中有一组队列控制方法，由 queue()/dequeue()/clearQueue() 三个方法组成。
- 主要应用于 animate()，ajax，其他要按时间顺序执行的事件中
```
var func1 = function(){alert('事件1');}
var func2 = function(){alert('事件2');}
var func3 = function(){alert('事件3');}
var func4 = function(){alert('事件4');}

// 入栈队列事件
$('#box').queue("queue1", func1);  // push func1 to queue1
$('#box').queue("queue1", func2);  // push func2 to queue1

// 替换队列事件
$('#box').queue("queue1", []);  // delete queue1 with empty array
$('#box').queue("queue1", [func3, func4]);  // replace queue1

// 获取队列事件（返回一个函数数组）
$('#box').queue("queue1");  // [func3(), func4()]

// 出栈队列事件并执行
$('#box').dequeue("queue1"); // return func3 and do func3
$('#box').dequeue("queue1"); // return func4 and do func4

// 清空整个队列
$('#box').clearQueue("queue1"); // delete queue1 with clearQueue
```
#### 谈一下Jquery中的bind(),live(),delegate(),on()的区别?
- bind 直接绑定在目标元素上
- live 通过冒泡传播事件，默认document上，支持动态数据
- delegate 更精确的小范围使用事件代理，性能优于 live
- on 是最新的1.9版本整合了之前的三种方式的新事件绑定机制
#### jQuery一个对象可以同时绑定多个事件，这是如何实现的?
```
 $("#btn").on("mouseover mouseout", func);

  $("#btn").on({
      mouseover: func1,
      mouseout: func2,
      click: func3
  });
```
#### 是否知道自定义事件。jQuery里的fire函数是什么意思，什么时候用?
- 事件即“发布/订阅”模式，自定义事件即“消息发布”，事件的监听即“订阅订阅”
- JS 原生支持自定义事件，示例：
    ```
        document.createEvent(type); // 创建事件
        event.initEvent(eventType, canBubble, prevent); // 初始化事件
        target.addEventListener('dataavailable', handler, false); // 监听事件
        target.dispatchEvent(e);  // 触发事件
    ```
- jQuery 里的 fire 函数用于调用 jQuery 自定义事件列表中的事件
#### jQuery 是通过哪个方法和 Sizzle 选择器结合的?(jQuery.fn.find()进入Sizzle)
- Sizzle 选择器采取 Right To Left 的匹配模式，先搜寻所有匹配标签，再判断它的父节点
- jQuery 通过 $(selecter).find(selecter); 和 Sizzle 选择器结合
#### 针对 jQuery性能的优化方法?
- 缓存频繁操作DOM对象
- 尽量使用id选择器代替class选择器
- 总是从#id选择器来继承
- 尽量使用链式操作
- 使用时间委托 on绑定事件
- 采用jQuery的内部函数data()来存储数据
- 使用最新版本的 jQuery
#### jQuery的源码看过吗?能不能简单说一下它的实现原理?
- (function(window, undefined) {})(window);
- jQuery 利用 JS 函数作用域的特性，采用立即调用表达式包裹了自身，解决命名空间和变量污染问题
- window.jQuery = window.$ = jQuery;
- 在闭包当中将 jQuery 和  暴露为全局变量
#### jQuery 中如何将数组转化为json字符串，然后再转化回来?
```
// 通过原生 JSON.stringify/JSON.parse 扩展 jQuery 实现
 $.array2json = function(array) {
    return JSON.stringify(array);
 }

 $.json2array = function(array) {
    // $.parseJSON(array); // 3.0 开始，已过时
    return JSON.parse(array);
 }

 // 调用
 var json = $.array2json(['a', 'b', 'c']);
 var array = $.json2array(json);
```

## 五、JS应用题目
#### 需求：实现一个页面操作不会整页刷新的网站，并且能在浏览器前进、后退时正确响应。给出你的技术实现方案?
1.用cookie或者localStorage来记录应用的状态即可，刷新页面时读取一下这个状态，后发送相应ajax请求来改变页面即可

2.HTML5里引用了新的API，就是history.pushState和history.replaceState，就是通过这个接口做到无刷新改变页面URL的

3.虽然ajax可以无刷新改变页面内容，但无法改变页面URL
4.其次为了更好的可访问性，内容发生改变后，改变URL的hash。但是hash的方式不能很好的处理浏览器的前进、后退等问题

5.有的浏览器引入了onhashchange的接口，不支持的浏览器只能定时去判断hash是否改变
再有，ajax的使用对搜索引擎很不友好，往往蜘蛛爬到的区域是空的

6.为了解决传统ajax带来的问题，HTML5里引入了新的API，即：history.pushState,history.replaceState
7.可以通过pushState和replaceState接口操作浏览器历史，并且改变当前页面的URL。
pushState是将指定的URL添加到浏览器历史里，replaceState是将指定的URL替换当前的URL。

- 如何调用
```
varstate = {    title: title, url: options.url,otherkey: othervalue};     window.history.pushState(state,document.title, url);
```
8.state对象除了要title和url之外，也可以添加其他的数据，比如：还想将一些发送ajax的配置给保存起来。

9.replaceState和pushState是相似的，不需要多做解释。
如何响应浏览器的前进、后退操作
10.window对象上提供了onpopstate事件，上面传递的state对象会成为event的子对象，这样就可以拿到存储的title和URL了。
```
indow.addEventListener('popstate',function(e){ if (history.state){    varstate = e.state; //do something(state.url, state.title); }}, false);
```
这样就可以结合ajax和pushState完美的进行无刷新浏览了。
#### 如何判断当前脚本运行在浏览器还是node环境中?
- this === window ? 'browser' : 'node';
通过判断Global对象是否为window，如果不为window，则当前脚本运行在node.js环境中。
#### 移动端最小触控区域是多大?
苹果推荐是 44pt x 44pt 「具体看 WWDC 14」，也可以看下面这个网址
https://developer.apple.com/ios/human-interface-guidelines/visual-design/layout/
#### jQuery 的 slideUp动画 ，如果目标元素是被外部事件驱动, 当鼠标快速地连续触发外部元素事件, 动画会滞后的反复执行，该如何处理呢?
- 在触发元素上的事件设置为延迟处理：使用 JS 原生 setTimeout 方法
在触发元素的事件时预先停止所有的动画，再执行相应的动画事件：$('.tab').stop().slideUp();
#### 把 script 标签 放在页面的最底部的body封闭之前 和封闭之后有什么区别?浏览器会如何解析它们?
- 按照 HTML 标准，在\</body>结束后出现\<script>或任何元素的开始标签，都是解析错误
虽然不符合 HTML 标准，但浏览器会自动容错，使实际效果与写在\</body>之前没有区别
浏览器的容错机制会忽略\<script>之前的\</body>，视作\<script>仍在 body 体内。省略\</body>和\</html>闭合标签符合 HTML 标准，服务器可以利用这一标准
#### 移动端的点击事件的有延迟，时间是多久，为什么会有? 怎么解决这个延时?
> click 有 300ms 延迟,为了实现safari的双击事件的设计，浏览器要知道你是不是要双击操作。
300ms。因为浏览器想看看你是不是要进行双击（double tap）操作。引入插件fastclick.js可以解决，Chrome浏览器在安卓设备上的时候，设置meta头信息中 user-scalable=no 但是这样就无法让用户多点触控缩放网页了。
https://blog.csdn.net/xjun0812/article/details/64919063
#### 知道各种JS框架(Angular, Backbone, Ember, React, Meteor, Knockout…)么? 能讲出他们各自的优点和缺点么?
- angular、backbone、knockout都是完整的MV*框架
- angular是双向数据绑定的，backbone、knockout是单向数据绑定的
- React只是单纯地View层
#### 什么是“前端路由”?什么时候适合使用“前端路由”? “前端路由”有哪些优点和缺点?
1.什么是前端路由？
- 路由是根据不同的 url 地址展示不同的内容或页面
- 前端路由就是把不同路由对应不同的内容或页面的任务交给前端来做，之前是通过服务端根据 url 的不同返回不同的页面实现的。

2.什么时候使用前端路由？
- 在单页面应用，大部分页面结构不变，只改变部分内容的使用
(前端路由主要用来替代ajax，可以使页面跳转时不刷新页面且地址栏相应变化）

3.前端路由有什么优点和缺点？
- 优点
用户体验好，不需要每次都从服务器全部获取，快速展现给用户
- 缺点
使用浏览器的前进，后退键的时候会重新发送请求，没有合理地利用缓存
单页面无法记住之前滚动的位置，无法在前进，后退的时候记住滚动的位置
#### 用js实现千位分隔符?
```
// 正则
function thousandBitSeparator(num) {
    return num && num
        .toString()
        .replace(/(\d)(?=(\d{3})+\.)/g, function($0, $1) {
            return $1 + ",";
        });
}
console.log(thousandBitSeparator(-1234567.9012));
// -1,234,567.9012
```
https://www.cnblogs.com/freeyiyi1993/p/4603525.html
#### 我们给一个dom同时绑定两个点击事件，一个用捕获，一个用冒泡，你来说下会执行几次事件，然后会先执行冒泡还是捕获。
- 先发生捕获事件，后发生冒泡事件。所有事件的顺序是：其他元素捕获阶段事件 -> 本元素代码顺序事件 -> 其他元素冒泡阶段事件 。
https://www.cnblogs.com/greatluoluo/p/5882508.html