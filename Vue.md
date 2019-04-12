## Vue

#### 是什么？

* 是一套用于构建用户界面的渐进式框架。
* 被设计为可以自底向上逐层应用
* 核心库只关注视图层
* 便于与第三方库或既有项目进行整合
* 与现代化工具链以及各种支持类库结合使用时，vue完全能够为复杂的单页应用提供驱动

#### 如何使用vue

* 可以创建一个.html文件，然后引入vue

  ```
  <!-- 开发环境版本，包含了有帮助的命令行警告 -->
  <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
  或者
  <!-- 生产环境版本，优化了尺寸和速度 -->
  <script src="https://cdn.jsdelivr.net/npm/vue"></script>
  ```

#### 核心是什么？

* 核心是允许采用简介的模板语法来声明地将数据渲染进DOM的系统

  ```
  <div id="app">
  	{{message}}
  </div>
  
  var app = new Vue({    //创建一个vue的实例对象挂载到指定的dom上
      el: '#app',   //是指元素挂载的节点
      data: {
          message:'Hello word'
      }
  })
  
  
  ```

#### 声明式渲染

```
<template>
  <div>
    <span :title="message">
      鼠标悬停查看动态绑定提示信息
    </span>
  </div>
</template>

<script>
export default {    //相当于提供一个接口给外界，让其他文件通过import来使                 
  name: 'home',     //export可以有多个import；export default仅有一个
  data () {
    return {
      message: '页面加载于 ' + new Date().toLocaleString()
    }
  }
}
</script>
```

* 该指令的意思是将这个节点的title特性和Vue实例的message属性保持一致

#### 条件与循环

```
//v-if控制的消失与显示
<template>
  <div>
    <p v-if="message">看到了</p>
  </div>
</template>

<script>
export default {
  name: 'home',
  data () {
    return {
      message:true    //相当于开关一样的东西
    }
  }
}
</script>
```

```
//v-for 实现的渲染功能
<template>
  <div>
    <ol>
    <li v-for="todo in todos" :key="todo.text">    //v-for要结合:key使用
      {{ todo.text }}                           //:key的使用主要是为了高效的更新虚拟DOM
    </li>                                          //key的值只能是number或者string类型
  </ol>
  </div>
</template>

<script>
export default {
  name: 'home',
  data () {
    return {
      todos: [
      { text: '学习 JavaScript' },
      { text: '学习 Vue' },
      { text: '整个牛项目' }
    ]
    }
  }
}
</script>
```

#### 处理用户输入

```
//v-on/@ 添加事件进行交互
<template>
  <div>
    <p>{{message}}</p>
    <button v-on:click="reverseMessage">逆转消息</button>
  </div>
</template>

<script>
export default {
  name: 'home',
  data () {
    return {
      message : "hello"
    }
  },

  methods:{
    reverseMessage : function () {
      this.message=this.message.split('').reverse().join()
      //split() 把一个字符串分割成字符串数组
      //reverse() 颠倒数组中的元素顺序
      //join() 把数组中元素所有元素放入一个字符串
    }
  }
}
</script>
```

```
//v-model 表单输入和应用状态之间的双向绑定
<template>
  <div>
    <p>{{message}}</p>
    <input type="text" v-model="message">
  </div>
</template>

<script>
export default {
  name: 'home',
  data () {
    return {
      message : "hello"
    }
  }
}
</script>
```

#### 组件化应用构建

* 一个组件本质上拥有预定义选项的一个实例

* 在Vue中注册组件：

  ```
  //创建一个组件并使用
  <template>
    <div>
      <todo-item></todo-item>
    </div>
  </template>
  
  <script>
  Vue.component('todo-item', {
    template: '<li>hi</li>'
  })
  export default {
    name: 'home',
    data () {
      return {
  
      }
    },
  }
  </script>
  ```

* 父传子

  ```
  <template>
    <div>
      <ol>
         <todo-item
      v-for="item in groceryList"
      :key="item.id"
      :todo="item"
      ></todo-item>
      </ol>
    </div>
  </template>
  
  <script>
  import Vue from 'vue'
  Vue.component('todo-item', {
    props:['todo'],
    template: '<li>{{todo.text}}</li>'
  })
  export default {
    name: 'home',
    data () {
      return {
        groceryList: [
        { id: 0, text: '蔬菜' },
        { id: 1, text: '奶酪' },
        { id: 2, text: '随便其它什么人吃的东西' }
      ]
      }
    },
  }
  </script>
  ```

  https://segmentfault.com/a/1190000014704088?utm_source=channel-hottest（父子组件之间传值）

#### 创建一个Vue实例

每个应用都是通过函数创建一个新的Vue实例开始的

```
var vm = new Vue({
  // 选项
})
```

#### 生命周期函数

* created/mounted/updated/destroyed
* 生命周期钩子的 `this` 上下文指向调用它的 Vue 实例 
* 钩子里不要使用箭头函数 



#### 模板语法

* 文本插值    {{}}    解释为的是普通文本     输出成html就要用v-html

* ```
  <span v-once>这个将不会改变: {{ msg }}</span>     //v-once 一次性的插值
  ```

* 提供JavaScript表达式的支持

  ```
  {{ number + 1 }}
  
  {{ ok ? 'YES' : 'NO' }}
  
  {{ message.split('').reverse().join('') }}
  
  <div v-bind:id="'list-' + id"></div>
  
  //注意不要写成语句
  ```




#### Webpack的主要优势

* 模块化开发（import，require） 
* 预处理（Less，Sass，ES6，TypeScript……） 
* 主流框架脚手架支持（Vue，React，Angular） 
* 庞大的社区（资源丰富，降低学习成本） 































