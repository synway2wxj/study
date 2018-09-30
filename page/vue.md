* npm install --global vue-cli
* vue init webpack my-project  cd my-project  npm run dev
* bower install vue
*     //邮箱正则判断    Vue.prototype.emailRel=function (email) {      var rel = /^[a-z0-9]+([._\-]*[a-z0-9])*@([a-z0-9]+[-a-z0-9]*[a-z0-9]+.){1,63}[a-z0-9]+$/;      if(rel.test(email)){        return true      }else {        return false      }    }
* //密码正则判断    Vue.prototype.passwordRel=function (psw) {      //至少6-15个字符，至少1个大写字母，1个小写字母和1个数字，其他可以是任意字符      var rel=/^(?=.*[a-z])(?=.*[A-Z])(?=.*\d)[\s\S]{6,15}$/      if(rel.test(psw)){        return true      }else {        return false      }    }
*     //设置cookie
    Vue.prototype.setCookie=function (name,value,times) {
      Cookies.set(name, value, { expires: parseInt(times)/24 });
    }
*     //获取cookie
    Vue.prototype.getCookie=function (name) {
      return Cookies.get(name)
    }
*     //删除cookie
    Vue.prototype.removeCookie=function (name) {
      return Cookies.remove(name)
    }
* //获取验证码倒计时    Vue.prototype.cutTime=function (event,time,callback) {      var target=event.target,_time=parseInt(time) || 60;      var set=setInterval(function () {        if(_time>0){          _time--;          target.innerHTML=_time;        }else {          target.innerHTML='获取手机验证码';          clearInterval(set);          callback();        }      },1000)    }
* //判断是否是ie9浏览器
    Vue.prototype.isIE_9=(navigator.userAgent.indexOf("MSIE 9.0")>0);
* //token 失效回到主页
    Vue.prototype.isLose=function () {
      if(!this.getCookie('token')){
        this.$router.push({path:"/"})
      }
    }
  }
*  vuex 类似于维护了一个全局的 Map对象。你可以往里存放 key-value 。然后所有的state数据操作都方法化，保证操作的可追踪和数据的干净
* vuex中的state存放的数据会丢失。因为它只是在当前页面初始化生成的一个实例，你一刷新页面所有数据重新生成，数据就没了。所以，vuex只能用于单个页面中不同组件（例如兄弟组件）的数据流通
* 事件修饰符once:prev:stop once只有一次被触发 prev不做跳转 stop时间停止器  @click.once v-on:mousemove.stop
* 当前dom变化幅度较大，如搜索时耗时，大量搜索，减少项目支出，优化项目，使用计算属性   当虚拟dom和真实dom不同时才触发计算属性方法。虚拟dom和真实dom相同，则不会触发计算属性的方法，而methods方法中内容不管如何都会触发全都
* v-bind:class="{changeColor}"
* <li v-for="character in characters">
                {{character}}
            </li>
* ES6语法
* 脚手架是通过webpack搭建的开发环境:使用ES6语法  打包和压缩JS为一个文件 项目文件在环境中编译，而不是浏览器 实现页面的自动刷新 要搭建脚手架，必须依赖的环境node.js
  npm install –global vue-cli  vue –version  vue init webpack my-project
  vue-router目前用不到，不必安装，有需要自定义安装
  ESLint测试，模式变的严谨，不必要
  npm run dev：开启一个8080端口，开展Vue项目
  assets：放置图片  components：放置组件    App.vue：根组件
  index.html入口文件，动态js插入到容器中，执行完index.html就会执行main.js中的内容，vue脚手架中从npm当中模块拿来使用
  全局组件不安全，在App.vue中设置局部组件，展示App.Vue中的子组件，完成组件嵌套
  * 组件CSS作用域
  <style scoped>
h1{
  color:purple;
}
* Vue有两种传值方式：父组件给子组件传值/子组件给父组件传值。对App.vue来说，Users.vue，Header.vue，Footer.vue都是他的子组件，所以父组件App.vue给子组件Users.vue传users数组值，子组件使用props接收值。type属性表示传递类型，required:true是否规格，指定对象和制定属性，不建议直接使用数组的方式
</style>
* 子组件$emit传值，父组件$event接受子组件的值
  this.$emit("titleChanged","子向父组件传值");
  <app-header v-on:titleChanged="updateTitle($event)" v-bind:title="title"></app-header>
* beforeCreate:function(){
    alert("组件实例化之前执行的函数");
  },
  created:function(){
    alert("组件实例化完毕，但页面还未显示");
  },
  beforeMount:function(){
    alert("组件挂载前，页面仍未展示，但虚拟Dom已经配置");
  },
  mounted:function(){
    alert("组件挂载后，此方法执行后，页面显示");
  },
  beforeUpdate:function(){
    alert("组件更新前，页面仍未更新，但虚拟Dom已经配置");
  },
  updated:function(){
    alert("组件更新，此方法执行后，页面显示");
  },
  beforeDestory:function(){
    alert("组件销毁前");
  },
  destoryed:function(){
    alert("组件销毁");
  }
  * 网络页面与页面之间的跳转，路由的性能优化的更好。使用路由机制不会实现请求与页面刷新，直接跳转
    npm install npm vue-router –save-dev
    import VueRouter from 'vue-router'
    Vue.use(VueRouter)

//配置路由
const router = new VueRouter({
    routes:[
        {path:"/",component:Home},
        {path:"/helloworld",component:HelloWorld},
    ],
    mode:"history"
})
* Vue自带的HTTP请求vue-resource
  npm install vue-resource -–save-dev
  import VueResource from 'vue-resource' 
  Vue.use(VueResource)
  created(){
    this.$http.get("http://jsonplaceholder.typicode.com/users").then((data) => {
    //  console.log(data);
    this.users = data.body;
    })
  }
* vue.js 不支持 IE8 及其以下版本，学习前请保证你的浏览器兼容 ECMAScript 5
* v-bind:id="vid" :class="vclass" :title="vtitle"   <h2>{{name.toLowerCase()}}</h2>
* v-on:submit.prevent="onSubmit"  v-bind:id="rawId | formatId"    {{ name | myfilters }}  :href="url"  @click="doSomething"
