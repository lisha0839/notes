# 几道迷惑性的js面试题

标签（空格分隔）： js 面试题

---

1、delete的用法
```
    (function(x){
        delete x;
        console.log(x);
    })(1)
```
答案为1。delete一般用于删除对象的属性，删除后其结果为undefined;但其不能删除变量。delete如果可以删除 返回true;不能删除返回false。
    如题，参数x为变量，不能使用delete删除
    
2、运算符
```
    var x=1;
    if(function f(){}){
        x += typeof f;
    }
    console.log(x)
    
    a:"1undefined"   b:"1function"
    c:NaN            d:报错
```
答案为"1undefined"。条件判断为假的情况有：0，false，''，null，undefined，未定义对象。函数声明写在运算符中，其为true，但放在运算符中的函数声明在执行阶段是找不到的。另外，对未声明的变量执行typeOf不会报错，会返回undefined

3、instanceof
```
   function f(){
        return f;
   }
   new f() instanceof f;
```
答案为"false"。a instanceof b 用于检测a是不是b的实例。如果题目f中没有return f,则答案明显为true;而在本题中new f()其返回的结果为f的函数对象，其并不是f的一个实例。

4、考眼力
```
  （function(foo){
        return typeof foo.bar;
  }）( {foo:{bar:1}} )
```
答案为"undefined"。传递进去的参数并没有bar属性

5、this
```
  var foo = {
		bar: function(){
            return this.baz;
        },
         baz:1
    }
	console.log(typeof (f=foo.bar)());
```
答案为"undefined"。将foo.bar赋值给f,相当于f(),故其this指向window






