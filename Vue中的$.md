### Vue中的$

* $set的使用
  * 可能遇到的情况：当生成vue实例后，再次给数据复制时，有时候并不会自动更新到视图上
  * 如果在实例创建之后添加新的属性到实例上，他不会触发视图更新
  * 调用方法
    * Vue.set(target,key,value)    /     this.$set(target,key,value)
      * target: 要更改的数据源（可以是对象或数组）
      * key: 要更改的具体数据
      * value: 重新附的值



* $emit的使用

  * 子组件调用父组件的方法并传递数据

  * 子组件标签中的事件不区分大小写，要用 “-” 隔开

  * 子组件

    ```
    <template>
      <button @click="emitEvent">点击我</button>
    </template>
    <script>
      export default {
        data() {
          return {
            msg: "我是子组件中的数据"
          }
        },
        methods: {
          emitEvent(){
            this.$emit('my-event', this.msg)
            //通过按钮的点击事件触发方法，然后用$emit触发一个my-event的自定义方法，传递this.msg数据。
          }
        }
      }
    </script>
    ```

  * 父组件

    ```
    <template>
      <div id="app">
        <child-a @my-event="getMyEvent"></child-a>
        <!--父组件中通过监测my-event事件执行一个方法，然后取到子组件中传递过来的值-->
      </div>
    </template>
    <script>
      import ChildA from './components/child.vue'
      export default {
        components: {
          ChildA
        },
        methods: {
          getMyEvent(msg){
              console.log('接收的数据--------->'+msg)//接收的数据--------->我是子组件中的数据
          }
        }
      }
    </script>
    ```



* $refs的使用

  * 父组件调用子组件的方法，可以传递数据

  * 子组件中的事件也不区分大小写，要用 “-” 隔开

  * 父组件

    ```
    <template>
      <div id="app">
        <child-a ref="child"></child-a>
        <!--用ref给子组件起个名字-->
        <button @click="getMyEvent">点击父组件</button>
      </div>
    </template>
    <script>
      import ChildA from './components/child.vue'
      export default {
        components: {
          ChildA
        },
        data() {
          return {
            msg: "我是父组件中的数据"
          }
        },
        methods: {
          getMyEvent(){
              this.$refs.child.emitEvent(this.msg);
              //调用子组件的方法，child是上边ref起的名字，emitEvent是子组件的方法。
          }
        }
      }
    </script>
    ```

  * 子组件

    ```
    <template>
      <button>点击我</button>
    </template>
    <script>
      export default {
        methods: {
          emitEvent(msg){
            console.log('接收的数据--------->'+msg)//接收的数据--------->我是父组件中的数据
          }
        }
      }
    </script>
    ```



* $on的使用

  * 兄弟组件之间相互传递数据

  * 首先穿件一个vue的空白实例（兄弟间的桥梁）

  * 父组件引入   childa,childb ->  `childa  $emit`发自定义事件参数  ->   `childb   $   $on`接收数据   

  * 子组件 childa    发送方使用$emit自定义事件把数据带过去

    ```
    <template>
        <div>
            <span>A组件->{{msg}}</span>
            <input type="button" value="把a组件数据传给b" @click ="send">
        </div>
    </template>
    <script>
    import vmson from "../../../util/emptyVue"
    export default {
        data(){
            return {
                msg:{
                	a:'111',
                	b:'222'
                }
            }
        },
        methods:{
            send:function(){
                vmson.$emit("aevent",this.msg)
            }
        }
    }
    </script>
    ```

  * 子组件  childb    接收方通过$on监听自定义事件的callback接受数据

    ```
    <template>
     <div>
        <span>b组件,a传的的数据为->{{msg}}</span>
     </div>
    </template>
    <script>
    	  import vmson from "../../../util/emptyVue"
    	  export default {
    		 data(){
    		        return {
    		            msg:""
    		        }
    		    },
    		 mounted(){
    		        vmson.$on("aevent",(val)=>{//监听事件aevent，回调函数要使用箭头函数;
    		            console.log(val);//打印结果：我是a组件的数据
    		            this.msg = val;
    		        })
    		  }
    	}
    </script>
    ```

  * 父组件：

    ```
    <template>
         <div>
          <childa></childa>	
          <br />
          <childb></childb>  	
         </div>
    </template>
    <script>
       import childa from './childa.vue';
       import childb from './childb.vue';
       export default {
       	components:{
       		childa,
       		childb
       	},
       	data(){
       		return {
       			msg:""
       		}
       	},
       	methods:{
       		
       	}
       }
    </script>
    ```

    