### JavaScript

#### 浅拷贝和深拷贝

* 浅拷贝：将原对象或原数组的引用直接赋给新对象，新数组，新对象／数组只是原对象的一个引用

  * 浅拷贝只是指向被复制的内存地址，原地址的对象发生改变，那么浅复制出来的值也会发生改变

* 深拷贝：创建一个新的对象和数组，将原对象的各项属性的“值”（数组的所有元素）拷贝过来，是“值”而不是“引用”

  * 开辟了一块内存地址用于存放复制的对象

* 浅拷贝和深拷贝的区别在于是否真正的获取了一个对象的复制而不是引用

  * 引用只发生在对象身上

    ```
    // 这种不算是深浅拷贝，只是复制
    var arr1=[1,2,3];
    var arr2=arr1;
    arr1.push(4);
    alert(arr1); //1234
    alert(arr2); //1234
    ```

  * slice(start,end)  不带参数相当返回新数组   从已有数组中截取一部分元素片段成新数组（不改变原数组）

    ```
    var array = [1, 2, 3, 4];
    var copyArray = array.slice();
    copyArray[0] = 100;
    console.log(array); // [1, 2, 3, 4]
    console.log(copyArray); // [100, 2, 3, 4]
    ```

  * concat() 用于连接两个或者多个数组    不改变原数组，返回一个被连接数组的副本

    ```
    var array = [1, 2, 3, 4];
    var copyArray = array.concat();
    copyArray[0] = 100;
    console.log(array); // [1, 2, 3, 4]
    console.log(copyArray); // [100, 2, 3, 4]
    ```

  * ES6

    ```
    // （1） Array.from(要复制的数组)  把一个类数组或者可遍历对象转换成一个真正的数组
    var arr1=[1,2,3];
    var arr2=Array.from(arr1);
    arr1.push(4);
    alert(arr1);  //1234
    alert(arr2);  //123
    
    // （2） ...扩展运算符  取出参数对象中所有可遍历属性拷贝到当前对象中
    var arr1=[1,2,3];
    var arr2=[...arr1];
    arr1.push(4);
    alert(arr1);  //1234
    alert(arr2);  //123
    
    // Object.assign(target, source1, source2) 用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target），并返回合并后的target
    var obj = {
    name: '彭湖湾',
    job: '学生'
    }
    var copyObj = Object.assign({}, obj);
    copyObj.name = '我才不叫彭湖湾呢！ 哼  (。・`ω´・)';
    console.log(obj);   // {name: "彭湖湾", job: "学生"}
    console.log(copyObj);  // {name: "我才不叫彭湖湾呢！ 哼  (。・`ω´・)", job: "学生"}
    ```

  * 不仅拷贝第一层级，还能够拷贝数组或对象所有层级的各项值

    不是单独针对数组或对象，而是能够通用于数组，对象和其他复杂的JSON形式的对象

    ```
    // JSON.parse(JSON.stringify(XXXX))  一招鲜吃遍天
        var array = [
            { number: 1 },
            { number: 2 },
            { number: 3 }
        ];
        var copyArray = JSON.parse(JSON.stringify(array))
        copyArray[0].number = 100;
        console.log(array); //  [{number: 1}, { number: 2 }, { number: 3 }]
        console.log(copyArray); // [{number: 100}, { number: 2 }, { number: 3 }]
     
     // 通过immutable引入的一套API，实现
     // 在改变新的数组（对象）的时候，不改变原数组（对象）
     // 在大量深拷贝操作中显著地减少性能消耗
     const { Map } = require('immutable')
     const map1 = Map({ a: 1, b: 2, c: 3 })
     const map2 = map1.set('b', 50)
     map1.get('b') // 2
     map2.get('b') // 50
    ```




#### 原生ajax

```
//1,new 
var oAjax = new XMLHttpRequest();

//2,open
oAjax.open('POST', url + '/user/register', false);//false表示同步请求

//3,setHeader,get请求不需要
oAjax.setRequestHeader("Content-type", "application/x-www-form-urlencoded");

//4，定义返回触发的函数，定义在send之前，不然同步请求就出问题
oAjax.onreadystatechange = function() {
    //6,通过状态确认完成
    if (oAjax.readyState == 4 && oAjax.status == 200) {
        //7,获取返回值，解析json格式字符串为对象
        var data = JSON.parse(oAjax.responseText);
    } else {
        console.log(oAjax);
    }
};

//，5发送，发送内容格式"a=1&b=2"，而不是json
oAjax.send('a=1&b=2');
```



#### call()和apply()

* 在这个之前要了解什么是执行上下文

  * 在写一个函数的时候会用到this，而这个this就是我们所说的执行上下文（执行环境）

    ```
    function fun() {
    	this.a = 1
    	console.log(this.a)
    }
    fun()
    console.log(window.a,'vvvvvv')
    ```

    this.a输出是1，window.a输出是1，所以this指向是window

* call的基本使用

  ```
  function.call(obj[,arg1[, arg2[, [,.argN]]]]])
  ```

  * 调用`call`的对象必须是个函数function

  *  `call`的第一个参数将会是function改变上下文后指向的对象,如果不传，将会默认是全局对象`window` 

  * 第二个参数开始可以接收任意个参数，这些参数将会作为function的参数传入function

  * 调用`call`的方法会立即执行

     

* apply()的使用

  ```
  function.apply(obj[,argArray])
  ```

  * 与`call`方法的使用基本一致，但是只接收两个参数，其中第二个参数必须是一个**数组**或者**类数组**，这也是这两个方法很重要的一个区别 

 

* call和apply()的异同点

  * 相同点：都能够改变方法的执行上下文，将一个对象的方法交给另一个对象来执行，并且是立即执行 

  * 异同点：参数个数，第二个参数形式

    ```
    // （1） call()方法
    function func (a,b,c) {}
    func.call(obj, 1,2,3)
    // function接收到的参数实际上是 1,2,3
    func.call(obj, [1,2,3])
    // function接收到的参数实际上是 [1,2,3],undefined,undefined
    
    // （2） apply()方法
    func.apply(obj, [1,2,3])
    // function接收到的参数实际上是 1,2,3
    
    func.apply(obj, {
        0: 1,
        1: 2,
        2: 3,
        length: 3
    })
    // function接收到的参数实际上是 1,2,3
    ```

*  何时用

  * 没有参数或者只有一个参数用call()，要传多个对象用apply()

* 改变this指向

  ```
  function funClass () {
      this.a = 1;
      this.p = function () {
          console.log(this.a);
      }
  }
  
  function classFun () {
      funClass.call(this);
      this.p();
  }
  
  classFun();
  // 1  继承了funClass的a和p方法
  ```

* 数组操作

  ```
  // 求数组最大值
  var a = [1,3,2,5,4,9,5,10]
  var max = Math.max.apply("",a)
  console.log(max)  // 10
  
  // 求数组最小值
  var min = Math.min.apply("",a)
  console.log(min)  // 1
  
  // 数组合并
  var arr1 = [2,4,6,8,10]
  var arr2 = [1,3,5,7,9]
  var arr3 = []
  arr3.push.call(arr3,arr1,arr2)
  console.log(arr3)
  // [[2,4,6,8,10],[1,3,5,7,9]]
  ```

  