#### ES6中常用的方法

##### let和const

* 不存在变量提升

  ```
  console.log(a)  // a is not defined
  let a = 6
  ```

* 块级作用域   {}

* 不能在同一作用域中重复声明

* const   声明只读常量



##### 数组的解构赋值

* 允许直接匹配赋值

  ```
  let [a, b, c] = [1, 2, 3]
  console.log([a,b,c]) // [1, 2, 3]
  ```

* 允许默认值

  ```
  let [a,b='1'] = ['2']; 
  console.log(a,b); // 2,1 
  
  let [a,b = '1'] = [2,undefined]; 
  console.log(b); // 1  ES6内部使用严格相等运算符'==='，严格等于undefined时,默认值生效
  
  let [a,b = '1'] = ['2',null]; 
  console.log(b); //null  默认值不生效，因为null不严格等于undefined
  ```

##### 对象的解构赋值

* 变量与属性同名

  ```
  let {a,b} = {a : "1",b : "2"}
  console.log(a); //1
  console.log(b); //2
  ```

* 变量与属性不同名

  ```
  let {a : name, b : age} = {a : 'jean', b : 18};
  console.log(name); // jean
  console.log(age);  // 18
  ```

##### 字符串解构

```
 let { length : len} = 'love you'
 console.log(len); // 8  类似数组的对象有length属性，可以对这个属性解构赋值
```



##### 模板字符串

传统模板使用’+‘拼接

* ES6采用（``）标识

  ```
  var data = lucy
  `jack love ${data}`;
  ```

* 若模板字符串中使用(``)需要用\转义

* 空格缩进都会被保留

  ```
  `<ul>
  	<li>1</li>
  	<li>2</li>
  	<li>3</li>
  </ul>`
  会有换行，如果不想要可以使用trim消除它
  ```

  

##### 函数默认值

```
function funName(name = 'zhangsan') {
    console.log(name)  
}
funName()  // zhangsan
funName('lisi')  // lisi
```



##### 箭头函数

```
var funName = val => val
等同于：
function(val) {
    return val
}
<------------------->
如果不需要参数或者多个参数则需要加括号
var funName1 = (val,index) => { return (val,index) }
<------------------->
如果直接返回一个对象，则在返回对象中加()
var funName1 = ({val,index}) => （{ val:zhangsan, index: 1 }）
```



##### 扩展对象

* 允许在对象中只写变量，则变量名=属性名

  ```
  (val,index) => ({ val,index })  // 等同于 return { val:val,index:index}
  ```

* Object.assign(target, source1, source2) 用于对象的合并，将源对象（source）的所有可枚举属性，复制到目标对象（target），并返回合并后的target

  ```
  var obj = {
  
      name: '张三',
  
      job: '学生'
  
  }
  // 浅拷贝方法
  var copyObj = Object.assign({}, obj);
  
  copyObj.name = '李四';
  
  console.log(obj);   // {name: "张三", job: "学生"}
  
  console.log(copyObj);  // {name: "李四", job: "学生"}
  
  ```



##### 模块功能

主要由两个命令构成：export和import

* export向外暴露接口

  ```
  export function funName() { ... }
  
  当只有一个默认函数时：
  export default function funName() { ... }
  ```

* import输入其他模块功能

  ```
  import fun from "./funName.js";
  ```



##### promise

它是异步操作	，有三种状态：pending（进行中）、fulfilled（成功）和rejected（失败）

两个特点：

* 只有异步操作的结果可以决定当前是哪个状态，不受其他外界因素影响
* 状态改变就不会在改变，再对这个对象进行操作，也不会有改变

```
var promise = new Promise(function(resolve, reject) {  
    let p = 12  
    if (p === 12){ // 成功
    resolve(p)
  } else { // 失败
    reject(p +1)
  }
})
```

##### async和 await

这是个ES7的拓展，让异步操作更方便

* async 异步的意思，相当于promise操作，定义的该函数不会阻塞后面代码的执行
* await 执行一个等待进程，是一个promise的返回结果

```
// 两则配合使用
async function funName() {
    var a = await('hello')
    return a
}
```



 

 

 