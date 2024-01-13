## 1.基础

### 1.1 JavaScript中的常量、变量及数据类型

------

常量（字面量）：数字和字符串

数字常量、字符串常量、布尔常量、自定义常量（const）

变量：var（ES6)之前，const、let（ES6)之后，变量如果只声明没初始化，值为undefined；

 **JS 的变量数据类型，是在程序运行的过程中，根据等号右边的值来确定的**。而且，变量的数据类型是可以变化的

JS的八大数据类型： （值）String、Number、Boolean、Null、Undefined、Symbol、BigInt、

​									(引用) Object 包括（Function、Array、Date、RegExp、Error）

```javascript
            var obj1=new Object();
            obj1.name='darling';
            var obj2=obj1;
            obj1.name='ending';
            console.log(obj1.name);
            console.log(obj2.name);
//两个值都变成ending
```

ES6的模板字符串${ },其中还可以写函数；

Number：有范围，超过了就变成infinity和-infinity  typeof都是number；

NaN:非数值，不正常的运算结果就是NaN;  typeof都是number;

变量的数据类型转换：

显示类型转换：

toString()

```javascript
<!DOCTYPE html>
<html lang="en">
<head>
      <meta charset="UTF-8">
      <meta http-equiv="X-UA-Compatible" content="IE=edge">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>Document</title>
</head>
<body>
      <script>
            //================================*toString()*==========================//
            const a="jdioahji";
            const b=298;
            const c=true;
            const d=[1,2,3];
            const e={name:'dafdfa',age:28};
            const f=null;
            const g=undefined;

            console.log(a.toString()); // "jdioahji"
            console.log(b.toString()); // "298"
            console.log(c.toString()); // "true"
            console.log(d.toString()); // "1,2,3"
            console.log(e.toString()); // "object"
            console.log(f.toString()); // Uncaught TypeError: Cannot read properties of null
            console.log(g.toString()); // Uncaught TypeError: Cannot read properties of undefined

            //tostring()可接受一个参数，将其转化位指定进制的string

             //================================*String()*==========================//

             //对于 Number、Boolean、String、Object 而言，本质上就是调用 toString()方法，返回结果同 toString()方法。
            //但是对于 null 和 undefined，则不会调用 toString()方法。它会将 null 直接转换为 "null"。将 undefined 直接转换为 "undefined"。

            //================================*Number()*==========================//

             const h="123";
             const i="   ";
             const j=true;
             const k=null;
             const l=undefined;
             console.log(Number(a));  //NaN
             console.log(Number(h));  //123
             console.log(Number(i));  //0
             console.log(Number(j));  //1
             console.log(Number(k)); //0
             console.log(Number(l)); // NAN

             //================================*parsreInt()*==========================//

             //parseInt()会将参数当作字符串来处理，由字符串转为int
             const m="123.45abf";
             console.log(parseInt(a));  //NaN
             console.log(parseInt(m));  //123
             console.log(parseInt(i));  //NaN
             console.log(parseInt(j));  //NaN
             console.log(parseInt(k));  //NaN
             console.log(parseInt(l)); //NaN

              //================================*Boolean()*==========================//

              Boolean(null)  //false
              Boolean(undefined)  //false
              Boolean([])  //true
              Boolean({})  //true

               //================================*isNaN()*==========================//
            
               //）先调用Number(参数)函数；
               console.log(isNaN('123')); // 返回结果：false。

              console.log(isNaN(null)); // 返回结果：false

              console.log(isNaN('abc')); // 返回结果：true。因为 Number('abc') 的返回结果是 NaN

              console.log(isNaN(undefined)); // 返回结果：true

              console.log(isNaN(NaN)); // 返回结果：true
      </script>
</body>
</html>
```

三个基本包装类，String()、Number()、Boolean()分别将对应的基本类型转化为String、Number、Boolean对象。

```javascript
const str=“keep”；
conole.log(str.length);
//将string转化为String，并调用length，在赋给原值，再置空对象；
```

String的常见方法：

```javascript
indexOf();
lastIndexOf();
//1.可填入字符串，eg：“jikh”；
//2.接受两个参数，第二个参数为查找的起始位置；

search();

includes();
//1.接受两个参数，第二个参数为查找的起始位置；
//2.找到与否不返回相应index、-1,而是true or false；

startWith();
endWith();
//1.接受两个参数，第二个参数为查找的起始位置（结束位置）；
//2.返回true false；

charAt(index);
str(index);
charCodeAt(index);
//1.index不在范内的话返回一个空字符串；
//2.charCodeAt()返回对应Unicode编码；

slice(lIndex，rIndex);
substring(lIndex，rIndex);
substr(index,length);
//1.返回对应位置的字符串
//2.包左不包右
//3.区别：slice对于（7，2）这样的传参返回“ ”，substring则当作(2,7)，substring不接受负数为参数；

String.fromCharCode();
//根据Unicode码获取字符串

concat();
//用于字符串的连接，等同于+；

split(分隔符);
//通过指定的分隔符将字符串转化为数组；

replace(oldStr,newStr);

repeat();
//返回字符串（指定重复次数的）；

trim();
//去除字符串前后的空白；

toLowerCase();
toUpperCase();





```

Number、Math的常见方法()

```javascript
Number.isInteger(a)   //返回bool值；
  
Number.toFixed(num)   //将Number保留num位小数，四舍五入，返回的是字符串；

const a=3.1415926;
conslole.log(a);
let b= a.toFixed(3);
conslole.log(b);  // 3.14;
conslole.log(tupeof b);  // string;


//============================*===============================//
//Math不需要new来调用，直接使用即可

//Math.PI	圆周率	Math对象的属性
//Math.abs()	返回绝对值	
//Math.random()	生成0-1之间的随机浮点数	取值范围是 [0，1)
//Math.floor()	向下取整（往小取值）	、、
//Math.ceil()	向上取整（往大取值）	
//Math.round()	四舍五入取整（正数四舍五入，负数五舍六入）	
//Math.max(x, y, z)	返回多个数中的最大值	
//Math.min(x, y, z)	返回多个数中的最小值	
//Math.pow(x,y)	乘方：返回 x 的 y 次幂	
//Math.sqrt()	开方：对一个数进行开方运算	
//举例：

    var num = -0.6;

    console.log(Math.abs(num));        //取绝对值

    console.log(Math.floor(num));      //向下取整，向小取

    console.log(Math.ceil(num));       //向上取整，向大取

    console.log(Math.round(num));      //四舍五入取整（正数四舍五入，负数五舍六入）

    console.log(Math.random());        //生成0-1之间的随机数


```

URI (Uniform ResourceIdentifiers,通用资源标识符)进行编码，以便发送给浏览器。有效的URI中不能包含某些字符，例如空格。而这URI编码方法就可以对URI进行编码，它们用特殊的UTF-8编码替换所有无效的字符，从而让浏览器能够接受和理解。

```js
    encodeURIComponent();   //把字符串作为 URI 组件进行编码
    decodeURIComponent();   //把字符串作为 URI 组件进行解码
```



举例：

```js
    var url = "http://www.cnblogs.com/smyhvae/";

    var str = encodeURIComponent(url);
    console.log(str);                           //打印url的编码
    console.log(decodeURIComponent(str));       //对url进行编码后，再解码，还原为url
```

Date：与Math不同，Date对象是一个构造函数，需要实例化后才能使用。

Date对象 有如下方法，可以获取日期和时间的**指定部分**：

| 方法名            | 含义              | 备注                 |
| ----------------- | ----------------- | -------------------- |
| getFullYear()     | 获取年份          |                      |
| getMonth()        | **获取月： 0-11** | 0代表一月            |
| getDate()         | **获取日：1-31**  | 获取的是几号         |
| getDay()          | **获取星期：0-6** | 0代表周日，1代表周一 |
| getHours()        | 获取小时：0-23    |                      |
| getMinutes()      | 获取分钟：0-59    |                      |
| getSeconds()      | 获取秒：0-59      |                      |
| getMilliseconds() | 获取毫秒          | 1s = 1000ms          |

**代码举例**：

```js
	// 我在执行这行代码时，当前时间为 2019年2月4日，周一，13:23:52
	var myDate = new Date();

	console.log(myDate); // 打印结果：Mon Feb 04 2019 13:23:52 GMT+0800 (中国标准时间)

	console.log(myDate.getFullYear()); // 打印结果：2019
	console.log(myDate.getMonth() + 1); // 打印结果：2
	console.log(myDate.getDate()); // 打印结果：4

	var dayArr  = ['星期日', '星期一', '星期二', '星期三', '星期四','星期五', '星期六'];
	console.log(myDate.getDay()); // 打印结果：1
	console.log(dayArr[myDate.getDay()]); // 打印结果：星期一

	console.log(myDate.getHours()); // 打印结果：13
	console.log(myDate.getMinutes()); // 打印结果：23
	console.log(myDate.getSeconds()); // 打印结果：52
	console.log(myDate.getMilliseconds()); // 打印结果：393

	//时间戳：的是从格林威治标准时间的1970年1月1日，0时0分0秒到当前日期所花费的毫秒数（1秒 = 1000毫秒）。
	
	var myDate = new Date("1970/01/01 0:0:0");

	console.log(myDate.getTime()); // 获取时间戳
```

### 1.2 数组

------

Array属于内置对象，同一个数组内，元素的类型可以不一致，

| 方法                             | 描述                                             | 备注             |
| -------------------------------- | ------------------------------------------------ | ---------------- |
| Array.isArray()                  | 判断是否为数组                                   |                  |
| toString()                       | 将数组转换为字符串                               | 不会改变原数组   |
| join()                           | 将数组转换为字符串，返回结果为**转换后的字符串** | 不会改变原数组   |
| 字符串的方法：split()            | 将字符串按照指定的分隔符，组装为数组             | 不会改变原字符串 |
|                                  |                                                  |                  |
| Array.from(arrayLike)            | 将**伪数组**转化为**真数组**                     |                  |
| Array.of(value1, value2, value3) |                                                  |                  |

### 数组元素的添加和删除

| 方法      | 描述                                                         | 备注           |
| --------- | ------------------------------------------------------------ | -------------- |
| push()    | 向数组的**最后面**插入一个或多个元素，返回结果为新数组的**长度** | 会改变原数组   |
| pop()     | 删除数组中的**最后一个**元素，返回结果为**被删除的元素**     | 会改变原数组   |
| unshift() | 在数组**最前面**插入一个或多个元素，返回结果为新数组的**长度** | 会改变原数组   |
| shift()   | 删除数组中的**第一个**元素，返回结果为**被删除的元素**       | 会改变原数组   |
|           |                                                              |                |
| splice()  | 从数组中**删除**指定的一个或多个元素，返回结果为**被删除元素组成的新数组** | 会改变原数组   |
| slice()   | 从数组中**提取**指定的一个或多个元素，返回结果为**新的数组** | 不会改变原数组 |
|           |                                                              |                |
| concat()  | 合并数组：连接两个或多个数组，返回结果为**新的数组**         | 不会改变原数组 |
| fill()    | 填充数组：用固定的值填充数组，返回结果为**新的数组**         | 会改变原数组   |

### 数组排序

| 方法      | 描述                                                    | 备注         |
| --------- | ------------------------------------------------------- | ------------ |
| reverse() | 反转数组，返回结果为**反转后的数组**                    | 会改变原数组 |
| sort()    | 对数组的元素,默认按照**Unicode 编码**，从小到大进行排序 | 会改变原数组 |

### 查找数组的元素

| 方法                  | 描述                                                         | 备注                                                     |
| --------------------- | ------------------------------------------------------------ | -------------------------------------------------------- |
| indexOf(value)        | 从前往后索引，检索一个数组中是否含有指定的元素               |                                                          |
| lastIndexOf(value)    | 从后往前索引，检索一个数组中是否含有指定的元素               |                                                          |
| includes(item)        | 数组中是否包含指定的内容                                     |                                                          |
| find(function())      | 找出**第一个**满足「指定条件返回 true」的元素                |                                                          |
| findIndex(function()) | 找出**第一个**满足「指定条件返回 true」的元素的 index        |                                                          |
| every()               | 确保数组中的每个元素都满足「指定条件返回 true」，则停止遍历，此方法才返回 true | 全真才为真。要求每一项都返回 true，最终的结果才返回 true |
| some()                | 数组中只要有一个元素满足「指定条件返回 true」，则停止遍历，此方法就返回 true | 一真即真。只要有一项返回 true，最终的结果就返回 true     |

### 遍历数组

| 方法      | 描述                                                         | 备注                                                         |
| --------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| for 循环  | 最传统的方式遍历数组，这个大家都懂                           |                                                              |
| forEach() | 遍历数组，但需要兼容 IE8 以上                                | 不会改变原数组。forEach() 没有返回值。也就是说，它的返回值是 undefined |
| for of    | 遍历数组（ES6语法）                                          | 不会改变原数组。另外，不要使用 for in 遍历数组               |
| map()     | 对原数组中的每一项进行加工，将组成新的数组                   | 不会改变原数组                                               |
| filter()  | 过滤数组：返回结果是 true 的项，将组成新的数组，返回结果为**新的数组** | 不会改变原数组                                               |
| reduce    | 接收一个函数作为累加器，返回值是回调函数累计处理的结果       | 比较复杂                                                     |

```js
//判断是否为数组,返回true false；
Array.isArray();

//数字转化为字符串；
Array.toString();
[1,3,5].toString();  //"1,3,5"
const a=string([1,3,5]);//"1,3,5"

const a=['a', 'b', 'c'];

a.join();   // 'a,b,c'
a.join(-); // 'a-b-c'
JSON.stringify(a) //['a','b','c'];

//字符串的方法
split()；
str.split(分隔符）;
//'a,b,c'  -->  ["a","b","c"];

//伪数组转化为真数组；
 const name='ljfljf';
 console.log(Array.from(name));//['l','j','f','l','j',f']

//创建数组
Array.of(1,'abc',true)；

//push返回的是新数组的长度；pop返回的是被删除元素；
//unshift(),前插，返回新数组长度，shift() 前删，返回被删除的元素；

//splice() 删除元素，返回新元素，并且改变原数组；原数组：没被删除的元素，新数组：删除元素；

Array.splice(startIndex);
Array.splice(startIndex,number);
Array.splice(startIndex,number,new1,new2,...); //新的元素占据被删除元素位置；
             
var arr1 = ['a', 'b', 'c', 'd', 'e', 'f'];
var result1 = arr1.splice(1); //从第index为1的位置开始，删除元素
console.log('arr1：' + JSON.stringify(arr1));
console.log('result1：' + JSON.stringify(result1));
//打印结果：
//arr1：["a"]
//result1：["b","c","d","e","f"]     
 
//slice() 提取指定索引元素；不改变原数组

//举例：

const arr = ['a', 'b', 'c', 'd', 'e', 'f'];

const result1 = arr.slice(); // 不加参数时，则获取所有的元素。相当于数组的整体赋值
const result2 = arr.slice(2); // 从第二个值开始提取，直到末尾
const result3 = arr.slice(-2); // 提取最后两个元素
const result4 = arr.slice(2, 4); // 提取从第二个到第四个之间的元素（不包括第四个元素）
const result5 = arr.slice(4, 2); // 空

console.log('arr:' + JSON.stringify(arr));
console.log('result1:' + JSON.stringify(result1));
console.log('result2:' + JSON.stringify(result2));
console.log('result3:' + JSON.stringify(result3));
console.log('result4:' + JSON.stringify(result4));
console.log('result5:' + JSON.stringify(result5));
//打印结果：
//arr: ['a', 'b', 'c', 'd', 'e', 'f'];
//result1: ['a', 'b', 'c', 'd', 'e', 'f'];
//result2: ['c', 'd', 'e', 'f'];
//result3: ['e', 'f'];
//result4: ['c', 'd'];
//result5: [];

//concat() //连接多个数组；参数可以多个数组；

//填充数组 fill()

// 用一个固定值填充数组。数组里的每个元素都会被这个固定值填充
新数组 = 数组.fill(固定值);

// 从 startIndex 开始的数组元素，用固定值填充
新数组 = 数组.fill(固定值, startIndex);

// 从 startIndex 到 endIndex 之间的元素（包左不包右），用固定值填充
新数组 = 数组.fill(固定值, startIndex, endIndex);
举例1：

// 创建一个长度为4的空数组，然后用 'f' 来填充这个空数组
console.log(Array(4).fill('f')); // ['f', 'f', 'f,' 'f']

// 将现有数组的每一个元素都进行填充
console.log(['a', 'b', 'c', 'd'].fill('f')); // ['f', 'f', 'f,' 'f']

// 指定位置进行填充
let arr1 = ['a', 'b', 'c', 'd'];
let arr2 = arr1.fill('f', 1, 3);

console.log(arr1); // ['a', 'f', 'f,' 'd']
console.log(arr2); // ['a', 'f', 'f,' 'd']

//reserve();反转

//sort()  排序，会改变原数组，返回的新数组和原数组一样；
//注意对Number型数组进行排序时，并不是字面的大小，因为是按照Unicode编码进行排序的；
let arr2 = [5, 2, 11, 3, 4, 1];

let result = arr2.sort(); // 将数组 arr2 进行排序

console.log('arr2 =' + JSON.stringify(arr2));
console.log('result =' + JSON.stringify(result));
//打印结果：
//arr2 =[1,11,2,3,4,5]
//result =[1,11,2,3,4,5]

//带参数时；

var arr = [5, 2, 11, 3, 4, 1];

// 自定义排序规则
var result = arr.sort(function (a, b) {
    if (a > b) {
        // 如果 a 大于 b，则交换 a 和 b 的位置
        return 1;
    } else if (a < b) {
        // 如果 a 小于 b，则位置不变
        return -1;
    } else {
        // 如果 a 等于 b，则位置不变
        return 0;
    }
});

console.log('arr =' + JSON.stringify(arr));
console.log('result =' + JSON.stringify(result));
打印结果：

arr = [1, 2, 3, 4, 5, 11];
result = [1, 2, 3, 4, 5, 11];
上方代码的写法太啰嗦了，其实也可以简化为如下写法：

//写法 2：（ES5写法）

var arr = [5, 2, 11, 3, 4, 1];

// 自定义排序规则
var result = arr.sort(function (a, b) {
    return a - b; // 升序排列
    // return b - a; // 降序排列
});

console.log('arr =' + JSON.stringify(arr));
console.log('result =' + JSON.stringify(result));
//打印结果不变。

//上方代码还可以写成 ES6 的形式，也就是将 function 改为箭头函数，其写法如下。

//写法 3：（ES6写法，箭头函数）

let arr = [5, 2, 11, 3, 4, 1];

// 自定义排序规则
let result = arr.sort((a, b) => {
    return a - b; // 升序排列
});

console.log('arr =' + JSON.stringify(arr));
console.log('result =' + JSON.stringify(result));
//上方代码，因为函数体内只有一句话，所以可以去掉 return 语句，继续简化为如下写法。

//写法 4：（推荐写法）

let arr = [5, 2, 11, 3, 4, 1];

// 自定义排序规则：升序排列
let result = arr.sort((a, b) => a - b);

console.log('arr =' + JSON.stringify(arr));
console.log('result =' + JSON.stringify(result));

//indexOf()、lastIndexOf()
//找到返回对应索引，否则-1；
//接受两个参数，第一个元素、第二个查找起始位置；
//查找法则相当于===；

//includes();
//找到为true，否则为false；
//接受两个参数，第二个参数是检索其实位置

//find()、findIndex();
//找到返回元素、元素索引；
//找不到返回undefined、-1；
let arr = [2, 3, 2, 5, 7, 6];

let result = arr.find((item, index) => {
    return item > 4; //遍历数组arr，一旦发现有第一个元素大于4，就把这个元素返回
  	// 上面这行代码是简写方式；完整写法也可以这样写：ccif (item > 4) {return true}
});

console.log(result); //打印结果：5

let result = arr.findIndex((item, index) => {
    return item > 4; //遍历数组arr，一旦发现有第一个元素大于4，就把这个元素的index返回
});

console.log(result); //打印结果：3

//every()、some();
var arr1 = ['千古', '宿敌', '南山忆', '素颜'];
var bool1 = arr1.every(function (item, index, array) {
    if (item.length > 2) {
        return false;
    }
    return true;
});
console.log(bool1); //输出结果：false。只要有一个元素的长度是超过两个字符的，就返回false

var arr2 = ['千古', '宿敌', '南山', '素颜'];
var bool2 = arr2.every(function (item, index, array) {
    if (item.length > 2) {
        return false;
    }
    return true;
});
console.log(bool2); //输出结果：true。因为每个元素的长度都是两个字符。

//遍历数组
// ES5语法
数组/boolean/无 = 数组.forEach/map/filter(function (item, index, arr) {
   相关代码和返回值；
})

// ES6语法
数组/boolean/无 = 数组.forEach/map/filter((item, index, arr) => {
   相关代码和返回值；
})


//for of   |   for in
//6语法推出了 for of，可用于循环遍历数组。
for(let value of arr) {
	console.log(value);
}
//使用 for in 遍历数组
//for in专门用于遍历对象的。对象的属性是无序的（而数组的元素有顺序），for in循环就是专门用于遍历无序的对象。所以，不要用 for in 遍历数组。

for in语法：

for (let key in obj) {
	console.log(key);
	console.log(obj.key);
}

//map()
const arr1 = [
    { name: '千古壹号', age: '28' },
    { name: '许嵩', age: '32' },
];

// 将数组 arr1 中的 name 属性，存储到 数组 arr2 中
const arr2 = arr1.map(item => item.name);

// 将数组 arr1 中的 name、age这两个属性，改一下“键”的名字，存储到 arr3中
const arr3 = arr1.map(item => ({
    myName: item.name,
    myAge: item.age,
})); // 将数组 arr1 中的 name 属性，存储到 数组 arr2 中

console.log('arr1:' + JSON.stringify(arr1));
console.log('arr2:' + JSON.stringify(arr2));
console.log('arr3:' + JSON.stringify(arr3));
打印结果：

arr1:[{"name":"千古壹号","age":"28"},{"name":"许嵩","age":"32"}]

arr2:["千古壹号","许嵩"]

arr3:[{"myName":"千古壹号","myAge":"28"},{"myName":"许嵩","myAge":"32"}]


//filter()
const arr1 = [
    { name: '许嵩', type: '一线' },
    { name: '周杰伦', type: '退居二线' },
    { name: '邓紫棋', type: '一线' },
];

const arr2 = arr1.filter((item) => item.type == '一线'); // 筛选出一线歌手

console.log(JSON.stringify(arr2));


//reduce() 回调特性，执行多次

// 定义方法：统一 value 这个元素在数组 arr 中出现的次数
function repeatCount(arr, value) {
    if (!arr || arr.length == 0) return 0;

    return arr.reduce((totalCount, item) => {
        totalCount += item == value ? 1 : 0;
        return totalCount;
    }, 0);
}

let arr1 = [1, 2, 6, 5, 6, 1, 6];

console.log(repeatCount(arr1, 6)); // 打印结果：3
```

### 1.3 函数

------



```js
//命名函数
function getmyFun([arg1,qrg2,]) {   }  //[]表示可选；

//匿名函数
const myFun = function() {   }

//函数的调用
getmyFun.call();
//或者作为对象的方法来调用

//定时器
setInternal(func() {},1000)

//js中实参的个数可以和形参个数不等。调用时不会检查实参类型
//不写return 返回undefined ；

//打印整个函数，console.log(myFun) 会打印整个函数
```

全局作用域，只有一个全局对象window，代表浏览器窗口，a相当于window.a,变量的作用域遵从就近原则。

变量/函数提升： JS在解析代码之前有一个预处理的过程，将当前的·所有变量的定义函数的定义放到代码最前面，所以在函数或变量定义的代码之前调用，并不会报错而是打印undefined，函数提示优先于变量提升 var定义变量才会提升，其他不会。

ES5中没有块级作用域。

js的运行三部曲

语法分析、预编译、解释执行

this，改变this指向，call()、bind()、apply()

### 1.4  闭包

------

函数外部访问函数内部作用域局部变量 closure，访问一内部函数就产生了闭包，这个内部函数称为闭包函数

```js
function f1() {
	const a=10;
	return function f2() {
			console.log(a);
	}
}

f1();
//在全局作用域中访问了f1的a
```

闭包的生命周期：

产生：内部函数f1被声明时，创建时而不是调用时就产生了；

死亡：嵌套的内部函数成为垃圾对象时，比如f1=null；

```
function f1() {
	var a=2;
	function f2() {
		a++;
		console.log(a);
	}
};
f1(); //3
f1(); //4

//说明闭包里面的数据并没消失；内部对象被调用了两次，但对象就创建了一个；

```

闭包的另外一种形式；

```js
function showDelay(msg,time) {
setTimeout(function() {
	alert(mag) 
},time)
}
//这个function是闭包，因为是嵌套的子函数，而且引用了外部函数的变量msg
```

闭包的作用：

1.延长局部变量的生命作用周期；

2.让函数外部可以操作函数内部的数据；

闭包的应用场景：

### 场景1：高阶函数

题目：不同的班级有不同成绩检测标准。比如：A班的合格线是60分，B 班的合格线是70分。已知某个人班级和分数，请用闭包函数判断他的成绩是否合格。

思路：创建成绩检测函数 checkStandard(n)，检查成绩 n 是否合格，函数返回布尔值。

代码实现：

```
// 高阶函数：判断学生的分数是否合格。形参 standardTemp 为标准线
function createCheckTemp(standardTemp) {
  // 形参 n 表示具体学生的分数
  function checkTemp(n) {
    if (n >= standardTemp) {
      alert('成绩合格');
    } else {
      alert('成绩不合格');
    }
  }
  return checkTemp;
}

// 创建一个 checkStandard_A 函数，它以60分为合格线
var checkStandard_A = createCheckTemp(60);
// 再创建一个 checkStandard_B 函数，它以70分为合格线
var checkStandard_B = createCheckTemp(70);

// 调用函数
checkStandard_A(65); // 成绩合格
checkStandard_B(65); // 成绩不合格
```



对于A班来说，它的闭包函数是createCheckTemp()，闭包范围是 checkTemp()函数和参数`standardTemp = 60`。对于B班来说，它的闭包函数是全新的createCheckTemp()，闭包范围是全新的checkTemp()函数和全新的参数`standardTemp = 70`。

因为有闭包存在，所以，并不会因为 createCheckTemp() 执行完毕后就销毁 standardTemp 的值；且A班和B班的standardTemp参数不会混淆。

备注：关于“高阶函数”的更多解释，我们在以后的内容中讲解。

### 场景2：封装JS模块

闭包的第二个使用场景是：定义具有特定功能的JS模块，将所有的数据和功能都封装在一个函数内部，只向外暴露指定的对象或方法。模块的调用者，只能调用模块暴露的对象或方法来实现对应的功能。

比如有这样一个需求：定义一个私有变量a，要求a只能被进行指定操作（加减），不能进行其他操作（乘除）。在 Java、C++ 等语言中，有私有属性的概念，但在JS中只能通过闭包模拟。

我们来看看下面的代码，如何通过闭包封装JS模块。

写法1：

（1）myModule.js：（定义一个模块，向外暴露多个方法，供外界调用）

```js
function myModule() {
    //私有数据
    var msg = 'Qinguyihao Haha'

    //操作私有数据的函数
    function doSomething() {
        console.log('doSomething() ' + msg.toUpperCase()); //字符串大写
    }

    function doOtherthing() {
        console.log('doOtherthing() ' + msg.toLowerCase()) //字符串小写
    }

    //通过【对象字面量】的形式进行包裹，向外暴露多个函数
    return {
        doSomething1: doSomething,
        doOtherthing2: doOtherthing
    }
}
```



上方代码中，外界只能通过doSomething1和doOtherthing2来操作里面的数据，但不让外界看到里面的具体实现。

（2）index.html:

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>闭包的应用-自定义JS模块</title>
</head>
<body>
<!--
闭包应用举例: 定义JS模块
  * 具有特定功能的js文件
  * 将所有的数据和功能都封装在一个函数内部(私有的)
  * 【重要】只向外暴露一个包含n个方法的对象或方法
  * 模块的使用者, 只需要调用模块暴露的对象或者方法来实现对应的功能
-->
<script type="text/javascript" src="myModule.js"></script>
<script type="text/javascript">
    var module = myModule();
    module.doSomething1();
    module.doOtherthing2();
</script>
</body>
</html>
```



写法2：

同样是实现上面的功能，我们还采取另外一种写法，写起来更方便。如下：

（1）myModule2.js：（是一个立即执行的匿名函数）

```js
(function () {
    //私有数据
    var msg = 'Qinguyihao Haha'

    //操作私有数据的函数
    function doSomething() {
        console.log('doSomething() ' + msg.toUpperCase())
    }

    function doOtherthing() {
        console.log('doOtherthing() ' + msg.toLowerCase())
    }

    //外部函数是即使运行的匿名函数，我们可以把两个方法直接传给window对象
    window.myModule = {
        doSomething1: doSomething,
        doOtherthing2: doOtherthing
    }
})()
```



（2）index.html：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>闭包的应用-自定义JS模块</title>
</head>
<body>
<!--
闭包的应用2 : 定义JS模块
  * 具有特定功能的js文件
  * 将所有的数据和功能都封装在一个函数内部(私有的)
  * 只向外暴露一个包信n个方法的对象或函数
  * 模块的使用者, 只需要通过模块暴露的对象调用方法来实现对应的功能
-->

<!--引入myModule文件-->
<script type="text/javascript" src="myModule2.js"></script>
<script type="text/javascript">
    myModule.doSomething1()
    myModule.doOtherthing2()
</script>
</body>
</html>
```



上方两个文件中，我们在`myModule2.js`里直接把两个方法直接传递给window对象了。于是，在index.html中引入这个js文件后，会立即执行里面的匿名函数。在index.html中把myModule直接拿来用即可。

## 

> 我们再讲两个概念，这两个概念和闭包有些联系。

内存泄漏

**内存泄漏**：**占用的内存**没有及时释放。

内存泄露的次数积累多了，就容易导致内存溢出。

**常见的内存泄露**：

1、意外的全局变量

2、没有及时清理的计时器或回调函数

3、闭包

情况1举例：

```js
// 意外的全局变量
function fn() {
  a = new Array(10000000);
  console.log(a);
}

fn();
```



情况2举例：

```js
// 没有及时清理的计时器或回调函数
var intervalId = setInterval(function () { //启动循环定时器后不清理
  console.log('----')
}, 1000)
js
// clearInterval(intervalId);  //清理定时器
```



情况3举例：

```js
function fn1() {
  var a = 4;
  function fn2() {
    console.log(++a)
  }
  return fn2
}
var f = fn1()
f()

// f = null //让内部函数成为垃圾对象-->回收闭包
```



### 内存溢出

**内存溢出**：程序运行时出现的错误。当程序运行**需要的内存**超过**剩余的内存**时，就抛出内存溢出的错误。

代码举例：

```js
    var obj = {};
    for (var i = 0; i < 10000; i++) {
    obj[i] = new Array(10000000);  //把所有的数组内容都放到obj里保存，导致obj占用了很大的内存空间
    console.log("-----");
    }
```



### 闭包是否会造成内存泄漏

一般来说，答案是否定的。因为内存泄漏是非预期情况，本来想回收，但实际没回收；而闭包是预期情况，一般不会造成内存泄漏。

但如果因代码质量不高，滥用闭包，也会造成内存泄漏。

## 闭包面试题

代码举例：

```js
function addCount() {
  let count = 0;
  return function () {
    count = count + 1;
    console.log(count);
  };
}

const fun1 = addCount();
const fun2 = addCount();
fun1();
fun2();

fun1();
fun2();
```



打印结果：

```
1
1
2
2
```



代码解释：

（1）fun1 和 fun2 这两个闭包函数是互不影响的，因此第一次调用时，count变量都是0，最终各自都输出1。

（2）第二次调用时，由于闭包有记忆性，所以各自会在上一次的结果上再加1，因此输出2。

### 1.5 面向对象

------

JS 中的面向对象，是基于**原型**的面向对象。JS 中的对象（Object）是依靠构造器（constructor）和原型（prototype）构造出来的。

另外，在ES6中，新引入了 类（Class）和继承（Extends）来实现面向对象。

使用 instanceof 可以检查**一个对象是否为一个类的实例**。

**语法如下**：

```
对象 instanceof 构造函数;
```



如果是，则返回 true；否则返回 false。

**代码举例**：

```js
function Person() {}

function Dog() {}

var person1 = new Person();

var dog1 = new Dog();

console.log(person1 instanceof Person); // 打印结果： true
console.log(dog1 instanceof Person); // 打印结果：false

console.log(dog1 instanceof Object); // 所有的对象都是Object的后代。因此，打印结果为：true
```



根据上方代码中的最后一行，需要补充一点：**所有的对象都是 Object 的后代，因此 任何对象 instanceof Object 的返回结果都是 true**。

如果对象里本身没有某个属性，则用点语法赋值时，这个属性会被创建出来。

如果属性名的命名规范没有遵循标识符的命名规范，就不能采用`.`的方式来操作对象的属性，则必须用方括号的形式来访问。比如说，`123`这种属性名，如果我们直接写成`obj.123 = 789`来操作属性，是会报错的。那怎么办呢？办法如下：

语法格式如下：（读取时，也是采用这种方式）

```js
// 注意，括号里的属性名，必须要加引号

// 获取属性
对象['属性名']

// 设置属性值
对象['属性名'] = 属性值;
```



上面这种语法格式，举例如下：

```js
obj['123'] = 789;

//删除对象属性
delete obj1.name;

//检查对象中是否有某属性
name in obj1;
if(obj1.name) {
    
}

```



数组、对象和map的遍历方式对比；for in 和 for of

```js
//for in
const array1 = ['a','b','c','d'];
const obj= {
    name:'ljf',
    age:27;
    height:175
}

for (const key in array1) //key值是数组的索引1，2，3, 遍历对象的话，是key值
for (const key of obj)   //报错，不可迭代类型，不能用for of 迭代，遍历数组的话，key是‘a','b'...
```

1.6 深拷贝和浅拷贝

```JS
      const obj2=Object.assign({},obj1)
      obj1.age=27
      obj1.pc.power=800
      console.log(obj1)
      console.log(obj2)
      
      //修改obj1的power会导致obj2的值也改变，非第一层，传的是引用；浅拷贝
      //第一层的age不会跟着变

      //浅拷贝只能拷贝第一层，其他的是拷贝引用；

      Object.assign(a,b) 
      //a中没有的属性b中有的话，会把属性附加到a上，有的话会被b覆盖
      Object.assign(a,b,c) 
```

![1702482202948](C:\Users\carpediem\AppData\Roaming\Typora\typora-user-images\1702482202948.png)

Object.freeze() 方法可以冻结一个对象。一个被冻结的对象再也不能被修改；冻结了一个对象则不能向这个对象添加新的属性，不能删除已有属性，不能修改该对象已有属性的可枚举性、可配置性、可写性，以及不能修改已有属性的值。此外，冻结一个对象后该对象的原型也不能被修改。freeze() 返回和传入的参数相同的对象。

代码举例：

```js
const params = {
    name: 'qianguyihao';
    port: '8899';
}

Object.freeze(params); // 冻结对象 params

params.port = '8080';// 修改无效
```



上方代码中，把 params 对象冻结后，如果想再改变 params 里面的属性值，是无效的。

```js
      const  a = 'fucking nivada yyyyy'
      let b=/a/
      let c =new RegExp('i','g')

      console.log(b.test(a))
      console.log(c.test(a))
      console.log(c.lastIndex)

      console.log(c.test(a))
      console.log(c.lastIndex)

      console.log(c.test(a))
      console.log(c.lastIndex)
```

![1702568750651](C:\Users\carpediem\AppData\Roaming\Typora\typora-user-images\1702568750651.png)

String对象的如下方法，是支持正则表达式的：

| 方法      | 描述                                                   | 备注 |
| --------- | ------------------------------------------------------ | ---- |
| split()   | 将字符串拆分成数组                                     |      |
| search()  | 搜索字符串中是否含有指定内容，返回索引 index           |      |
| match()   | 根据正则表达式，从一个字符串中将符合条件的内容提取出来 |      |
| replace() | 将字符串中的指定内容，替换为新的内容并返回             |      |

```js
      var str = "1a2b3c4d5e6f7g";
      let a=str.split(/[A-Z]/)
      let b=str.search(/c[234]d/)
      let c=str.match(/[A-z]/)
      let d=str.match(/[A-z]/g)
      console.log(a)
      console.log(b)
      console.log(c)
      console.log(d)
      console.log(str.replace(/e/,'$%%%'))
```

### 1.6 DOM(Document Object Model)

------

节点的概念，一切都是节点，HTML\、文本、属性、标签

```js
var div1 = document.getElementById("box1"); //方式一：通过 id 获取 一个 元素节点（为什么是一个呢？因为 id 是唯一的）

var arr1 = document.getElementsByTagName("div"); //方式二：通过 标签名 获取 元素节点数组，所以有s

var arr2 = document.getElementsByClassName("hehe"); //方式三：通过 类名 获取 元素节点数组，所以有s

//获取节点
Node.parentNode
节点.nextElementSibling || 节点.nextSibling
节点.previousElementSibling || 节点.previousSibling
节点.firstElementChild || 节点.firstChild
节点.lastElementChild || 节点.lastChild
父节点.childNodes
节点.children

 document.createElement("li"); 
父节点.appendChild(新的子节点);  //最后
父节点.insertBefore(新的子节点,作为参考的子节点)
父节点.removeChild(子节点);
要复制的节点.cloneNode();       //括号里不带参数和带参数false，效果是一样的。
要复制的节点.cloneNode(true);   //子节点也复制进去了
元素节点.属性名; myNode.src
元素节点[属性名]; myNode['className']
元素节点.getAttribute("属性名称");
元素节点.setAttribute("属性名", "新的属性值");
元素节点.removeAttribute("属性名");

//对于非原始元素，.[]和getAttribute不能混用

//nodeType == 1 表示的是元素节点（标签） 。记住：在这里，元素就是标签。

//nodeType == 2 表示是属性节点。

//nodeType == 3 是文本节点。

```

浏览器在加载一个页面时，是按照自上向下的顺序加载的，读取到一行就运行一行。如果将script标签写到页面的上边，在代码执行时，页面还没有加载，页面没有加载DOM对象也没有加载，会导致无法获取到DOM对象。

**onload 事件**：

onload 事件会在整个页面加载完成之后才触发。为 window 绑定一个onload事件，该事件对应的响应函数将会在页面加载完成之后执行，这样可以确保我们的代码执行时所有的DOM对象已经加载完毕了。

### 1.7 style 行内样式

------

```js
 box1.style.width = "300px";
 box1.style.backgroundColor = "red"; // 驼峰命名法
```

行内样式有较高的优先级，但是如果其他地方写了！important ，则此处会有更高的优先级，style是对象

```js
box.style.cssText
//把行内样式里的值当作字符串来对待
box1.style.cssText = "width: 300px;height: 300px;background-color: green;";
```

获取当前正在使用的样式

（1）w3c的做法：

```js
    window.getComputedStyle("要获取样式的元素", "伪元素"); //第二个参数可传null,返回的是对象
```



两个参数都是必须要有的。参数二中，如果没有伪元素就用 null 代替（一般都传null）。

（2）IE和opera的做法：

```js
    obj.currentStyle;  // ele.currentStyle[attr]
```

```js
//行内样式和offset

dom.offsetHeight;
dom.offsetWeight;
dom.offsetLeft;  //相对父元素的偏移量，从padding算起；
dom.offsetTop;
dom.offsetParent;
//返回的是number，对于无父元素的dom，则以body为准；style.height返回的是字符串；
```

### 1.8 scroll相关属性和缓动动画

------

scrollHight、scrollWidth

滚动条的高宽，如果内容不超过盒子，就等于盒子大小，否则等于实际大小

scrollTop、scrollLeft

滚动条往上、左滚动的距离

判断进度条是否到底部或最右边；

scrollHeight - scrollTop=clientHeight；

scrollWidth-scrollLeft=clientWidth；

获取html文档的方法：

doucument.titile;

document.body;

document.head

document.documentElement;

client家族的组成

clientHeight、clentWidth：可供元素和body调用，元素时包括padding，只读，不可更改，返回的是数字；

clientX、clientY:鼠标距可视区域左、上侧的距离；

clientTop、clentLeft：盒子的上、左border；

offset、scroll、client的区别：

1.offsetHeight、scrollHeight、clientHeight的区别：scroll多了border；

2.offsetTop、scrollTop、clientY的区别：offset是距离父盒子的定位距离，clientY为event调用，

```js
window.screen.width "    " + window.screen.height
//获取分辨率
```

1.9 事件的绑定和事件对象

------

way1:onclick,同一个元素的同一个事件只能绑定一个响应函数，否则后者会覆盖前者；

way2：addEventListener();不会覆盖，都会执行，不支持IE8及以下浏览器；三个参数，最后一个为触法时间段，默认false（冒泡时），true为捕获时；

way3： attachEvent（IE8以下浏览器），不会覆盖，后绑定的先执行；

事件对象：

当事件的响应函数被触发时，会产生一个事件对象，浏览器每次会将这个事件event作为实参传进之前的响应函数，这个对象中包含了事件相关的信息，etc：鼠标的坐标、事件的时间戳等；

![img](https://camo.githubusercontent.com/c0983e76897d718f4db2f16a904fe6669b296271545329cdc2bc287ed01007db/687474703a2f2f696d672e736d79687661652e636f6d2f32303138303230335f313733392e706e67)

DOM事件流：

事件传播的三个阶段：事件捕获、事件冒泡、目标

捕获阶段：从DOM树结构中找，直到获取到事件目标target，这个阶段监听函数是不会被触发的；

事件目标: 到达目标元素后，执行相应的处理函数；

冒泡阶段：从事件目标target开始，从子元素往祖先元素冒泡，直到页面的最上一级标签；

![img](https://camo.githubusercontent.com/6dc3dcf8dff8643224f662f03b4f69120ec34aab8830529643d5f94995c07faf/687474703a2f2f696d672e736d79687661652e636f6d2f32303138303230345f313231382e6a7067)

捕获：window --> document --> html--> body --> 父元素、子元素、目标元素。有两个对象最常用：window、doucument。它们俩是最先获取到事件的
冒泡：div->body->html->document->window

子元素的事件被触发时，父元素的同样的事件也会被触发

以下事件不冒泡：blur、focus、load、unload、onmouseenter、onmouseleave。意思是，事件不会往父元素那里传递。

我们检查一个元素是否会冒泡，可以通过事件的以下参数：

```js
    event.bubbles

//阻止冒泡，
event.cancelBubble = true
//如果返回值为true，说明该事件会冒泡；反之则相反。
```

事件委托：是把一个元素响应事件（click、keydown......）的函数委托到另一个元素。

鼠标的拖拽事件：onMousedown，onMousemove，onMouseup；

鼠标的滚轮事件：onmousewheel；

键盘事件：onkeydown，onkeyup；

1.9 BOM(Browser Object Model)

- Window：代表整个浏览器的窗口，同时 window 也是网页中的全局对象。
- Navigator：代表当前浏览器的信息，通过该对象可以识别不同的浏览器。
- Location：代表当前浏览器的地址栏信息，通过 Location 可以获取地址栏信息，或者操作浏览器跳转页面。
- History：代表浏览器的历史记录，通过该对象可以操作浏览器的历史记录。由于隐私原因，该对象不能获取到具体的历史记录，只能操作浏览器向前或向后翻页，而且该操作只在当次访问时有效。
- Screen：代表用户的屏幕信息，通过该对象可以获取用户的显示器的相关信息。

### 1.9 原型对象

------

每一个对象里面的方法都是独一无二的，创建1000个对象，即使对象的类型相同，那么对象的方法也有1000份，为了节省空间，可以利用原型，在对象内写共用的方法

```js
function Person(name,age,gender) {
    this.name=name;
    this.age=age;
    this.gender=gender;
    this,sayName=function() {
        console.log(this.naem)
    }
}

//比较好的方法：
Person.prototype.sayName=function() {
        console.log(this.naem)
    }
```

我们创建的函数，解析器都会向函数中添加一个prototype属性，这个属性对应着一个对象，就是原型对象，普通函数调用原型无任何作用，当作为构造函数来调用时，就能访问该函数的原型，访问方法：

```js
Person.prototype;
var per1=new Person();
per1._proto_

//两种方法方法
```

使用 `in` 检查对象中是否含有某个属性时，如果对象中没有但是**原型中**有，也会返回true。

可以使用对象的`hasOwnProperty()`来检查**对象自身中**是否含有该属性。

原型对象也是对象，所以它也有原型，当我们使用或访问一个对象的属性或方法时：

- 它会先在对象自身中寻找，如果有则直接使用；
- 如果没有则会去原型对象中寻找，如果找到则直接使用；
- 如果没有则去原型的原型中寻找，直到找到Object对象的原型。
- Object对象的原型没有原型，如果在Object原型中依然没有找到，则返回 null