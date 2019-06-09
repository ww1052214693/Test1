# 1.组件之间的传值问题

- ##### 父组件向子组件传值

  ```javascript
  //父组件
  //引入子组件
  <子组件 :msg=msg></子组件>
  
  data() {
      return {
          msg:'我是父组件中的内容'
      }
  }
  
  
  
  
  //子组件
  //此时  this.msg  中就是父组件传过来的值
  props:{
      msg:{
          type:String
      }
  }
  ```

- ##### 子组件向父组件传值

  ```javascript
  //子组件
  
  this.$emit('父组件中的自定义事件名',要传的值) ==> 实例:  this.$emit('accept',type)
  
  
  
  
  //父组件
  //引入子组件
  //这里的 accept 就是  上述子组件中的 '父组件中的自定义事件名'这个参数
  <子组件 @accept=son></子组件>  
  
  data(){
      return {
          num:0
      }
  }
  
  methods:{
      //accept的自定义事件的事件函数
      son(type) {
          this.num = type     //这里的 type 作为参数,由子组件传过来,然后将值赋给父组件的这个 num 属性
      }
  }
  ```

- ##### 兄弟组件之间传值

  ```javascript
  //首先在父组件中引入俩子组件  组件A 和 组件B
  //组件A  传值给  组件B
  //此时需要中间桥梁连接这俩组件
  
  //在assets文件夹中创建一个 bus.js 文件,里面的代码如下:
  
  import vue from 'vue'
  exports default new vue
  
  
  
  //组件A
  //先引入 bus.js 文件
  import bus from '路径'
  
  data(){
      return {
          msg:"我是A组件中的内容"
      }
  }
  methods:{
      //为此组件上的某个元素注册点击事件,事件函数为这个
      sendMsg(){
          bus.$emit('send',this.msg)   //this.msg 为要传的值
      }
  }
  
  
  //组件B
  //先引入 bus.js
  import bus from '路径'
  data(){
      return {
          num:''
      }
  }
  
  created(){
      var self = this
      bus.$on('send',function(val){    //通过 $on 接收传过来的值
          //注意这里this的指向有变化
          self.num = val     //这个 val 就是传过来的值
      })
  }
  
  
  
  ```

  