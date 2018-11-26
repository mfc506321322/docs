# 阿里巴巴笔试+面试

##  阿里面试考查知识点
安全方面就是你讲的那些xss,csrf，sql注入。还有react路由设计原理，webpack,双向绑定，redux数据流。加分项有es6的装饰器，generator，tcp原理，git flow, 其他的就是那本面试题上大部分都有。

##  阿里笔试题经典案例
###  1. ES6
#### 1.1关于Class
::: tip Question:
阿里云产品线十分丰富，拥有ECS、RDS等数百款产品，每个产品都具有一些通用属性，例如：ID（id），地域（region），名称（name），同时每个产品又包含自己特有的属性。 ECS拥有实例（instance）属性，可选值有ecs.t1.small、ecs.t3.small、ecs.t1.large RDS拥有数据库类型（dbType）属性，可选值有mysql、mssql、PPAS 请使用你的面向对象知识，基于ES6语法编写ECS、RDS两个类，并实现如下方法： 1. config() 返回一个字面量对象，可以拿到所有的成员变量。 2. buy() 返回一个URL，格式https://www.aliyun.com/buy?id=xxx&region=xxx&name=xxx&每个产品自己特有的成员变量
:::
```js
class Base{
	constructor(options){
		this.id = options.id || '';
		this.region = options.region || '';
		this.name = options.name || '';
	}
	config(){
		return {
			id: this.id,
			name: this.name,
			region: this.region
		}
	}
	buy(){
		return `https://www.aliyun.com/buy?id=${this.id}&region=${this.region}&name=${this.name}`
	}
}

class ECS extends Base{
	constructor(options){
		super(options);
		if (['ecs.t1.small', 'ecs.t3.small', 'ecs.t1.large'].indexOf(options.instance) != -1){
			this.instance = options.instance	
		}else{
			this.instance = '';
		}
	}
	config(){
		return Object.assign({}, super.config(), {instance: this.instance});
	}
	buy(){
		return `${super.buy()}&instance=${this.instance}`
	}
}

class RDS extends Base{
	constructor(options){
		super(options);
		if (['mysql', 'mssql', 'PPAS'].indexOf(options.dbType) != -1){
			this.dbType = options.dbType	
		}else{
			this.dbType = '';
		}
	}
	config(){
		return Object.assign({}, super.config(), {dbType: this.dbType});
	}
	buy(){
		return `${super.buy()}&dbType=${this.dbType}`
	}
}

let ecs = new ECS({name:'ecs',id:1,region:'华北',instance:'ecs.t3.small'})
ecs.config();
ecs.buy();

let rds = new ECS({name:'rds',id:2,region:'华东',dbType:'PPAS'})
rds.config();
rds.buy();
```
#### 1.2 关于promise
:::tip Question:
实现图片的依次加载和并行加载
:::
```js
// 封装加载图片的promise
let loadImg = (src)=>{
    return new Promise((resolve, reject)=>{
        let img = new Image();
        img.onload = ()=>{
            resolve(img);
        }
        img.onerror = ()=>{
            reject(new Error());
        }
    })
}
const imgs = ['url1', 'url2', 'url3'];
// 依次加载图片
async function fSync(){
    for (let i=0,len=imgs.length; i<len; i++){
        let img = await loadImg(imgs[i]);
        document.body.appendChild(img);
    }
}
// 并行加载图片
function fAsync(){
    imgs.forEach(async item=>{
        let img = await loadImg(imgs[i]);
        document.body.appendChild(img);
    })
}
```

### 2.DOM树在内存中的表示及JSX的遍历
::: tip Question: 
请用递归的方式遍历树形数据结构中的每一个节点
:::
```js
const options = [
  {
    value: 'zhejiang',
    label: 'Zhejiang',
    children: [
      {
        value: 'hangzhou',
        label: 'Hangzhou',
        children: [
          {
            value: 'xihu',
            label: 'West Lake'
          }
        ]
      }
    ]
  },
  {
    value: 'jiangsu',
    label: 'Jiangsu',
    children: [
      {
        value: 'nanjing',
        label: 'Nanjing',
        children: [
          {
            value: 'zhonghuamen',
            label: 'Zhong Hua Men'
          }
        ]
      }
    ]
  }
];
// 深度优先遍历
function eachOpt(option){
	option.forEach(element => {
		console.log('element value....',element.value)
		if(Array.isArray(element.children) && element.children.length){
        	eachOpt(element.children)
      	}
   	});
}
eachOpt(options)
```

### 3. 字符串的基础操作
:::tip Question:
在开发中，我们经常会碰到将abc-xyz这类格式的字符串转为AbcXyz形式的驼峰字符串进行处理，
例如：hello-world我们希望能够变成驼峰风格的HelloWorld，请编写代码实现这个camelize(str)方法 
:::
```js
function camelize(str) {
    //补充代码
  var strArr = str.split('-');
  return strArr.map(item=>{
  	let upperCase = item[0].toUpperCase();
  	return upperCase+item.slice(1)
  }).join('');
}
camelize('hello-world');
```

### 4.函数的节流与原生事件
:::tip Question:
请用js实现一个监听浏览器窗口变化的函数，当浏览器窗口的宽度大于等于 600px 
的时候console.log('hello')（持续大于等于600px的话打印一次即可），请用你觉得最优的实现
:::
```js
var throttle = function(func, ms){
    var start = +new Date();
    
    return function(){
        var now = +new Date();
        if (now- start > ms){
            setTimeout(function(){
                func();
            }, ms);
            start = now;
        }

    }
}

var flag = false;
var resizeFunc = throttle(function(){
    if (!flag && window.innerWidth >= 600){
        console.log('hello');
        flag = true;
    }else if(window.innerWidth < 600){
        flag = false;
    }
}, 300);

window.addEventListener('resize', resizeFunc);
```

### 4.关于排序
#### 4.1 二分排序
:::tip Question
写一个有效的算法完成矩阵搜索，这个矩阵有如下特点：
    1) 矩阵中的每行数字都是经过排序的，从左到右依次变大。
    2) 每行的第一个数字都比上一行的最后一个数字大
例如：
[
    [2,   4,  8,  9],
    [10, 13, 15, 21],
    [23, 31, 33, 51]
]
实现一个函数，搜索这个数组
输入：4，返回：true
输入：3，返回：false
:::
```js
const arr =  [
    [2,   4,  8,  9],
    [10, 13, 15, 21],
    [23, 31, 33, 51]
];



// 一维数组二分法查找
function searchArray(arr, num){
    console.log('arr...', arr, num);
    let len = arr.length;
    if (arr[0] > num || arr[len-1] < num){
        return false;
    }else {
        let mid = Math.floor(arr.length/2);
        if (arr[mid] > num){
            return searchArray(arr.slice(0, mid), num);
        }else if(arr[mid] < num){
            return searchArray(arr.slice(mid+1, len), num);
        }else{
            return true;
        }
    }
}

// 二维数组二分查找
function search(arr, num){
    console.log('arr..', arr);
    let len = arr.length,
        arrLen = arr[0].length;
    let middle = Math.floor(arr.length/2);
    if (arr[0][0] > num || arr[len-1][arrLen-1] < num){
        return false;
    }else{
        if (arr[middle][0] > num ){
            // 当最小值大于num，在前面查找
            return search(arr.slice(0, middle), num);
        }else if(arr[middle][arrLen-1] < num){
            // 当最大值小于num，在后面查找
            return search(arr.slice(middle+1, len), num);
        }else{
            // 在这中间，调用一维数组查找方法
            return searchArray(arr[middle], num);
        }
    }
}
let result = search(arr, 52);
console.log('查询结果...', result);
```
#### 4.2 快速排序
```js
let arr1 = [1,23,7,5,3,2,8,2,19,99,10,12,17,78,87];
function quickStart(arr){
    let mid = Math.floor(arr.length/2);
    let left = [],
        right = [];
    // 递归终止条件
    if (arr.length <= 1){
        return arr;
    }
    arr.forEach(item=>{
        if (item > arr[mid]){
            right.push(item);
        }else if(item < arr[mid]){
            left.push(item);
        }
    })
    return quickStart(left).concat([arr[mid]], quickStart(right));
}
console.log('排序前', arr1, '排序后：', quickStart(arr1));
```
#### 4.3 冒泡排序
```js
let arr1 = [1,23,7,5,3,2,8,2,19,99,10,12,17,78,87];
function bubble(arr){
    for (let i=0, len=arr.length; i<len; i++){
        for (let j=i+1, len=arr.length; j<len; j++){
            let tmp = 0;
            if (arr[i] > arr[j]){
                tmp = arr[i];
                arr[i] = arr[j];
                arr[j] = tmp;
            }
        }
    }
    return arr;
}
console.log('排序前', arr1, '排序后：', bubble(arr1));
```