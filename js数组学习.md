# js数组学习

标签（空格分隔）： js、数组

---

本文是对数组的常规方法做一个记录。
数组的基本方法除concat\slice外都会对原数组进行修改
##数组的创建
```
    var arr = new Array(12);// 创建一个长度为12的数组，值为undefined
    var arr1 = new Array(1,2,3); 
    var arr2 = [1,2,3]; //arr1=arr2
```
##length
数组的长度可以读取，也可设置
```
var arr = [1,2,3];
arr.length;  //3
arr.length=0; //[]
```
##Array.indexOf('value',index)
**作用**：在数组中查找给定元素（从左往右找）
**参数**：value-要查找的值；index-从第index位开始查找；index省略从头开始搜索,负数代表相对数组末尾的偏移量
**返回值**：找到，返回第一个匹配元素的索引；没有找到返回-1
```
    var arr=[1,2,3,4,2,3];
    arr.indexOf();//=>-1
    arr.indexOf(2,1);//=>1
    arr.indexOf(2,7);//=>-1
    arr.indexOf(5);//=>-1
    arr.indexOf(2,-2);//=>4
    arr.indexOf(2,-6);//=>1 负数超出范围都找的1
    arr.indexOf(2,-11);//=>1 从第-5位往右找
```
查找数组中所有的x,并返回其下标
```
<!--
    @a:要查找的字符串
    @arr:要查找的数组
-->
function findAll(x,arr){
    var i=0;
    var results=[];
    while(arr.indexOf(x,i) != -1){
        results.push(arr.indexOf(x,i));
        i = arr.indexOf(x,i)+x.length;
    }
    return results;
}
```
##Array.lastIndexOf('value',index)
**作用**：在数组中查找给定元素（从右往左找）
**参数**：value-要查找的值；index-从第index位开始查找；index省略从尾开始搜索,负数代表相对数组末尾的偏移量
**返回值**：找到，返回第一个匹配元素的索引；没有找到返回-1
```
    var arr=[1,2,3,4,2,3];
    arr.lastIndexOf();//=>-1
    arr.lastIndexOf(2,1);//=>1
    arr.lastIndexOf(2,0);//=>-1
    arr.lastIndexOf(2,7);//=>4 正数超出范围都找的是4
    arr.lastIndexOf(2,-2);//=>4 从第4位往左找
    arr.lastIndexOf(2,-6);//=>-1 从第0位往左找
    arr.lastIndexOf(2,-11);//=>-1 从第-5位往左找
```
##Array.join('value')
**作用**：将数组转为字符串
**参数**：value-数组元素间连接符；省略时默认为（，）
**返回值**：一个字符串。将数组中每个元素转化为字符串，并用value值衔接起来
```
    var arr=[1,2,3];
    arr.join();//=>"1,2,3"
    arr.join('');//=>"123"
    var arr1=new Array(3);
    arr1.join('-'); //=>"--"
```
##Array.concat('value')
**作用**：衔接数组
**参数**：value-可以是一个元素或一个数组(数组取的是元素)
**返回值**：一个衔接value的新数组。不会修改调用的数组
```
    var arr=[1,2,3];
    arr.concat(4,5);//=>[1,2,3,4,5]
    arr.concat([4,5]);//=>[1,2,3,4,5]
    arr.concat([4,[5,[6,7]]]);//=>[1,2,3,4,[5,[6,7]]]
```
##Array.push()、Array.pop()、Array.shift()、Array.unshift()
**作用**：
    1.添加元素: 返回新数组长度
    >push:数组末尾添加元素；
    unshift:数组开头添加元素;一次性插入
    
2.删除元素: 返回删除的数据
    >pop:删除数组最后一个元素；
    shift:删除数组第一个元素;
```
    var arr=[1,2,3];
    arr.push([4,5]);//=>[1,2,3,[4,5]]  返回4
    arr.shift();//=>[2,3,[4,5]]  返回1
```
##Array.slice(start,end)
**作用**：返回数组一部分
**参数**：start-开始序号，end-结束序号。end省略默认到最后一位。负数从数组尾部开始计算，-1表示最后一位，-2表示倒数第二位
**返回值**：start到end之间的新数组[start,end)。不会修改调用的数组
```
    var arr=[1,2,3,4,5];
    arr.slice(0,3);//=>[1,2,3]
    arr.slice(3);//=>[4]
    arr.slice(1,-1);//=>[2,3,4]
    arr.slice(-3,-2);//=>[3]
    arr.slice(-8,3);//=>[1,2,3]
    arr.slice(3,0);//=>[]  截取不到返回空数组，从小到大，不交换
```
##Array.splice(start,deleteCount,value,...)
**作用**：添加、删除和替换数组元素
**参数**：start-数组元素序号
      deleteCount-要删除元素的个数
      value-要插入数组中的0个或多个值
**返回值**：删除元素返回包含删除元素的新数组；
        添加或替换返回空数组
```
    var arr=[1,2,3,4,5,6,7,8];
    arr.splice(4);//=>返回[5,6,7,8]a为[1,2,3,4]
    arr.splice(1,0,2,3);//=>返回[] a为[1,2,3,2,3,4]
    arr.splice(1,1,5);//=>返回[2] a为[1,5,3,2,3,4]
```
##Array.sort(orderfunc)
**作用**：对数组元素排序
**参数**：可选函数。不带参数按字符编码排序
```
    arr.sort(function(a,b){
        return a-b; //从小到大
        //return b-a; 从大到小
       // return Math.random()-0.5; 随机排序
    })
```
##Array.reverse()
**作用**：颠倒数组元素，逆序
```
   var arr=[1,2,3];
   arr.reverse(); //[3,2,1]
```
##Array.toString()
**作用**：将数组转为字符串，与join不传参数一样
**参数**：可选函数。不带参数按字符编码排序
```
   [1,2,3].toString(); //"1,2,3"
   [1,[2,'c']].toString(); //"1,2,c"
```
-------
#ESCMAScript中数组方法
均不会改变原数组
##Array.forEach()
**作用**：遍历数组，为每个元素调用指定函数
**注意**：forEach不能在所有元素传递给函数前终止遍历
```
   var arr=[1,2,3]; 
   arr.forEach(function(item,index,arr){
        arr[index] = item+1;
   })
   arr=>[2,3,4]
```
##Array.map()
**作用**：将数组每个元素传递给用指定函数
**注意**：传递给map的函数应有返回值，不修改原数组，返回的是新数组
```
   var arr=[1,2,3]; 
   b=arr.map(function(item,index,arr){
        return x*x;
   })  //[1,4,9]
```
##Array.filter()
**作用**：返回过滤后数组的一部分
```
    删除数组中undefined和null
    a = a.filter(function(item){
        return item!==undefined && item!==null;
    })
```
##Array.every()
**作用**：对数组元素应用指定函数进行检测
**返回值**：所有元素均满足条件，返回true；否则false
**注意**：every和some一旦能确认返回什么值，就会停止遍历
```
    var arr = [1,2,3]
    arr.every(function(item){
        return item<5;
    }) //true
```
##Array.some()
**作用**：对数组元素应用指定函数进行检测
**返回值**：有一个元素满足条件，返回true
**注意**：空数组，调用every()返回true;调用some返回false
##Array.reduce(fn,value)
**作用**：使用指定函数将数组进行组合，返回一个值（从左往右）
**参数**：fn-指定函数，value-传递给函数的初值
一个参数：
> 第一次的两个值分别为数组的第一、二个元素，其结果作为第二次的第一个值

两个参数：
>第一次的值为value和数组第一个元素，其结果作为第二次的第一个值
```
    var arr = [1,2,3，4,5]
    var sum = arr.reduce(function(prev,cur,index,arr){
        return prev+cur;
    },0)
    var max = arr.reduce(function(x,y){
    return (x>y)?x:y;
    })
```
##Array.reduceRight(fn,value)
**作用**：使用指定函数将数组进行组合，返回一个值（从右往左）

--------------------------
#ES6对数组方法的扩展（）

参考http://es6.ruanyifeng.com/#docs/array
##Array.form(arr,fn)
**作用**：将类数组对象和可遍历对象转为真正的数组。如nodeList、argument等
**参数**：arr为类数组或集合，fn函数作用类似map方法
**注意**：只要部署了Iterator接口的数据结构，都能将其转为数组。字符串和set结构都可以转为数组
```
   let arrLike={
    '0':'a',
    '1':'b',
    '2':'c',
    length:3
   }
   var arr1=[].slice.call(arrLike); //es5
   var arr2=Array.from(arrLike);
   Array.form([1,2,3],(x)=>x*x) //[1,4,9]
   Array.form('abc'); //['a','b','c']
```
##Array.of(value)
**作用**：将一组值转为数组,弥补Array()因参数的个数不同结果不同的不足
```
  Array(3) //[,,,]  Array.of(3) //[3]
  Array() //[]  Array.of() //[]
```
##Array.fill(value，start,end)
**作用**：使用给定的value,填充一个数组
**参数**：value要填充的值，start-end从start到end进行填充
```
 [1,2,3].fill(5); //[5,5,5]
 [1,2,3].fill(4,1,2); //[1,4,3]
```
-------------------------
#数组检测
使用typeOf可以完成对基本数据类型的检测，对数组的检测可以使用以下方法：
>1、Array.isArray([]) =>true
2、[] instanceOf Array =>true
instanceOf问题：web浏览器可能右多个窗口或frame，每个窗口都有自己的JavaScript环境，有自己的全局对象。每个全局对象有自己的构造函数，因此一个窗体中的对象不可能是另一个窗口的构造函数实例， 因此该方法存在一定的问题
3、Object.prototype.toString.call([]) == "[object Array]"; =>true
call()和apply()都可以间接地调用函数，并显式地修改this值。任何函数都可以作为任何对象的方法来调用，哪怕这个函数不是那个对象的方法。如：
```
    Array.join = Array.join || function(a,sep){
        return Array.prototype.join.call(a,sep);
    }
    Array.prototype.join.call('abc','-'); //a-b-c
```

