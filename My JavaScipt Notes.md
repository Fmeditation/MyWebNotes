1.基础

1.1 

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