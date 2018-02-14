### 数据类型的核心操作原理

***数据类型:***

   1.基本数据类型:
> - number:
> - string:
> - boolean:
> - null
> -undefined

   2.引用数据类型:
> - Object
> - function  


 js代码之所以能运行在浏览器中,是因为浏览器给我们提供了一个供js运行的环境,我们称为"全局作用域",在前端中,我们用window来表示.node或者后台里面的全局作用域是global

```javascript
   
    var a=2;
    var b=a;
    b=3;
    console.log(a)-----  2
-------------------------------------
   var a={name:"xiaojin",job:"js"}
   var b=a;
   b={"name":"lili"}  
   cosole.log(a.name)-----xiaojin
  ------------------------------------
  var a={name:"xiaojin",job:"js"}
   var b=a;
   b.name="lili"
   cosole.log(a.name)-----lili

   
```
3.数组求和

```javascript
   function  total(){
      var total=null;
      var ary=Array.prototype.slice.call(arguments); //转化为类数组
      return eval(ary.join("+"))
   }
```
4.函数:
 > + 每个函数可以执行无数次,每次执行都互不干扰(但有时存在间接关系)

  function fn(){} 

  fn() //每次执行都相当于copy了一份
  
  + 形成的私有作用域,把私有变量保护起来了,在私有作用域中,操作私有变量和外界无关,外界无法直接操作私有变量,把这种机制叫做"闭包"

  fn()

5.堆内存 和栈内存

  ***栈内存:***  
      栈内存俗称"作用域"(全局作用域,私有作用域)
 >  -  为js执行提供一个环境(js执行代码的地方)
 >  -  基本数据的值直接存在栈内存

 私有作用域,当私有作用域执行完毕后,没有占用的,就会销毁.全局作用域,当网页关闭的时候就会销毁
***堆内存***
    
 >  - 存放的是引用数据类型的地址,当我们不用的时候可以把引用数据类型指向null空指针
      var obj={"name":"lili"};
      var a=obj;
      obj=null //当不再需要obj的时候,就可以这样,便于浏览器把空闲的内存销毁.

##变量提升之篇章(即预解释)##
  变量提升在`当前作用域中`,js自上而下执行,浏览器首先会把所有带`var 或者function`关键字的进行提前的`声明或者定义`
 > - 声明:在当前作用域中`吼一嗓子`,我有num这个变量了.var num

 > - 定义:赋值  num=12


> var 的时候只是声明,function 是声明和定义都完成了.我们看下面的例子

```javascript

console.log(num)
var num=12;
console.log(num)
console.log(fn)
function fn(){
  console.log(a)
  var a=12
  console.log(a)
}
console.log(fn())
```
> + 定义变量时候带var 和不带var 的区别
  
     在全局作用域下,我们var num=12;就相当于给window添加了一个属性名num,window.num=12
     在...........,我们num=12,给上面一样,但是由于没var 就相当于没声明,在赋值前面打印num 会报错
     
     下面的例子都是相当于给window添加了一个属性num  window.num=12;但是一个有声明一个没声明

     
  ```javascript
     console.log(num)----报错`num is not defined`
     num=12;
     console.log(num)-----12
  ```
 ```javascript
    
    console.log(num)----undefined  进行了预解释
    var num=12;
     console.log(num)-----12
 ```
  作用域链
========

>    函数执行会形成一个私有作用域,首先变量提升,然后执行代码

>  -  执行的时候遇到一个私有变量,按照私有变量处理即可

>  - 如果不是私有的,就得向上一级作用域查找,如果没找到继续一级一级找,找到停止,直到到window为止.这种查找机制叫做`作用域链`.

>  如果上级作用域有,操作的就是上级作用域的变量,如果在当前作用域改了值,就相当于改了上一级的值.
   
   下面我们来看一个作用域实例:

```javascript
   console.log(x,y)-----全局作用域,声明了,==="undefined"
   var x=10,y=20;

   function fn(){
     console.log(x,y)  //私有作用域,只声明了x,所以x 是私有,x==="undefined",私有作用域没有y,上级查找window,y就是全局作用域
     var x=y=100;   //此步骤把y全局作用域的值改变了100
     console.log(x,y)=====100  100
   }
   console.log(x,y)=====x:10   y:100
```
    
  ***变量提升需要注意的几个点***
  >  -  只对"="左边的进行预解释,右边不进行
  >  -  不管条件是否成立都要进行预解释
  >  -  重命名下的处理





































