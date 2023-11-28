# My Vue Notes



## 1.VUE的系统指令

### **1.1 插值表达式{{ msg}}**

------



```vue
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ name == 'smyhvae' ? 'true' : 'false' }}

{{ message.split('').reverse().join('') }}
```

但只能包含单个表达式

### **1.2 v-cloak**

------

`v-cloak`：保持和元素实例的关联，直到结束编译后自动消失。eg:{{name}}，当网速慢时页面会一直显示name，到加载完成后才会显示name对应的值，使用v-cloak后，未加载完成前会一直隐藏name直到加载完成再显示

### 1.3 **v-text**

------

v-text可以将一个变量的值渲染到指定的元素中。

v-text可以将一个变量的值渲染到指定的元素中。例如：

```vue
  <!-- 插值表达式 -->
  <span>content:{{name}}</span>

  <!-- v-text -->
  <span v-text="name">/span>
```

**区别1**： v-text 没有闪烁的问题，因为它是放在属性里的。

**区别2** :插值表达式只会替换自己的这个占位符，并不会把整个元素的内容清空。v-text 会**覆盖**元素中原本的内容。

为了解释区别2，我们来用代码举例：

```vue
  <!-- 插值表达式 -->
  <p>content:++++++{{name}}------</p>

  <!-- v-text -->
  <p v-text="name">------++++++</p>
```

第二行代码中，只要浏览器中还没有解析到`v-text="name"`的时候，会显示`------++++++`；当解析到`v-text="name"`的时候，name的值会直接替换`------++++++`。

### **1.4 v-html**

------

`v-text`是纯文本，而`v-html`会被解析成html元素。

```vue
        <p>{{msg}}</p>
        <p v-text="msg"></p>
        <p v-html="msg"></p>
....
        data:{
        return {
        mag:'<h1>我是一个大大的h1标题</h1>'
        }
        }
```

### 1.5 v-bind

------

`v-bind`：用于绑定**属性**。

```vue
<img v-bind:src="imageSrc +'smyhvaeString'">

<div v-bind:style="{ fontSize: size + 'px' }"></div>
```

上方代码中，给属性加了 v-bind 之后，属性值里的整体内容是**表达式**，属性值里的`imageSrc`和`size`是Vue实例里面的**变量**。

也就是说， v-bind的属性值里，可以写合法的 js 表达式。

### 1.6 v-on 

------

事件绑定机制

```vue
<template>
  <div id="div1">
    {{isFirst}}
</div>
<span v-cloak>{{ nacdaiu }}</span>
<span v-text="isFirst"></span>
<div>
  <button @click="showname"></button>
</div>
</template>

<script lang="ts">
export default {
  name:'app',
  data() {
    return {
      isFirst:'cassdw',
      nacdaiu:false,
    }
  },
  methods:{
    showname() {
     this.isFirst+='k'
    }
  }
}
</script>
```

`v-on` 提供了很多事件修饰符来辅助实现一些功能。事件修饰符有如下：

- `.stop` 阻止冒泡。本质是调用 event.stopPropagation()。
- `.prevent` 阻止默认事件（默认行为）。本质是调用 event.preventDefault()。
- `.capture` 添加事件监听器时，使用捕获的方式（也就是说，事件采用捕获的方式，而不是采用冒泡的方式）。
- `.self` 只有当事件在该元素本身（比如不是子元素）触发时，才会触发回调。
- `.once` 事件只触发一次。
- `.{keyCode | keyAlias}` 只当事件是从侦听器绑定的元素本身触发时，才触发回调。
- `.native` 监听组件根元素的原生事件。

PS：一个事件，允许同时使用多个事件修饰符。

stop和capture例子如下，没有stop修饰时，点击子元素，父元素事件也会被点击，当父元素加上capture修饰时，顺序从冒泡改成直接捕获。

self例子，给父元素加上self标签，点击子标签时便不会冒泡，只有点击父元素本身才会触发相应事件。

```vue
<template>
  <div class="father" @click="showFTips">
  <div  class="child" @click.stop="showCTips"></div>
</div>
</template>
<script lang="ts">
export default {
  name:'app',
  data() {
    return {
    }
  },
  methods:{
    showFTips() {
      console.log('father clicked')
    },
    showCTips() {
      console.log('child clicked')
    }
  }
}
</script>
<style>
[v-cloak] {
  display: none;
}
.father {
            height: 300px;
            width: 300px;
            background: pink;
        }

        .child {
            width: 200px;
            height: 200px;
            background: green;
        }
</style>

```

prevent例子，加了prevent关键字后跳转和打印只会执行prevent修饰的打印

```vue
<template>
  <div class="father">
    <a href="http://www.hikvision.com" @click.prevent="showFTips">goto</a>
</div>
</template>
<script lang="ts">
export default {
  name:'app',
  data() {
    return {
    }
  },
  methods:{
    showFTips() {
      console.log('father clicked')
    },
  }
}
</script>
<style>
[v-cloak] {
  display: none;
}
.father {
            height: 300px;
            width: 300px;
            background: pink;
        }
</style>

```

**DEMO:文字滚动显示**

------

```vue
<template>
  <div>
    <p v-text="message"></p>
  </div>
  <div>
  <button @click="showLEDconteent">开始</button>
  <button @click="stopInternal">停止</button>
</div>
</template>

<script lang="ts">
export default {
  name:'app',
  data() {
    return {
      message:'international 就一定要实现',
      internalId:0
    }
  },
  methods:{
    showLEDconteent() {
      if(this.internalId!=0) {
        return
      }
      this.internalId=setInterval(()=>{
          const startMsg=this.message.substring(0,1)
          const endMsg=this.message.substring(1)
          this.message=endMsg+startMsg
      },400)
    },
    stopInternal() {
      clearInterval(this.internalId)
      this.internalId=0
    }
  }
}
</script>

<style>
[v-cloak] {
  display: none;
}
</style>

```

- 在Vue的实例中，如果想要获取data里的属性、methods里面的方法，都要通过`this`来访问。这里的**this指向的是Vue的实例对象**。
- VM实例，会监听自己身上 data 中所有数据的改变，只要数据一发生变化，就会自动把最新的数据，从 data 上同步到页面中去。这样做 的好处是：**程序员只需要关心数据，不需要考虑如何重新渲染DOM页面；减少DOM操作**。
- 在调用定时器 id 的时候，代码是`this.intervalId`，防止定时器多开。
- - **v-model 双向数据绑定**

  ------

  **区别**：

  - v-bind：只能实现数据的**单向**绑定，从 M 自动绑定到 V。
  - v-model：只有`v-model`才能实现**双向**数据绑定。注意，v-model 后面不需要跟冒号，、

  **注意**：v-model 只能运用在**表单元素**中，或者用于自定义组件。常见的表单元素包括：input(radio, text, address, email....) 、select、checkbox 、textarea。

  例中还涉及样式通过属性的绑定方法，以对象或数组的形式

```vue
<template>
  <div class="father">
    <input class="num first" type="text" v-model="n1">
    <select v-model="opt">
      <option value="+">+</option>
      <option value="-">-</option>
      <option value="*">*</option>
      <option value="/">/</option>
    </select>
    <!-- 对象写法 -->
    <!-- <input :class="{
      num: true, first: true
    }" type="text" v-model="n2"> -->
    <!-- 数组写法 -->
    <input type="text" :class="['num','first']" v-model="n2">
    <input type="button" value="=" @click="calc">
    <input type="text" v-model="result">
</div>
</template>
<script>
export default {
  name:'app',
  data() {
    return {
      n1:'',
      n2:'',
      result:'',
      opt:'+'
    }
  },
  methods: {
    calc() {
      switch (this.opt) {
        case '+':
          this.result = String(parseInt(this.n1) + parseInt(this.n2))
          break;
        case '-':
          this.result = String(parseInt(this.n1) - parseInt(this.n2))
          break;
        case '*':
          this.result =String( parseInt(this.n1) * parseInt(this.n2))
          break;
        case '/':
          this.result = String(parseInt(this.n1) / parseInt(this.n2))
          break;
        default: 
          break
      }
    },
  }
}
</script>
<style>
  .num {
    background-color: green;
  }
  .first {
      height: 60px;
  }
</style>


```

### **1.7 v-for的四种使用方式**

------

way1：普通数组的遍历

```vue
 
data: {
  arr1: [2, 5, 3, 1, 1],
}
<li v-for="item in arr1">{{item}}</li>
<!-- 括号里如果写两个参数：第一个参数代表值，第二个参数代表index 索引 -->
<li v-for="(item,index) in arr1">值：{{item}} --- 索引：{{index}}</li>
```

way2：对象数组的遍历

```vue
data: {
//对象数组
dataList: [
{ name: 'smyh', age: '26' },
{ name: 'vae', age: '32' },
{ name: 'xiaoming', age: '20' }
]
}
<!-- 对象数组的遍历。括号里如果写两个参数：第一个参数代表数组的单个item，第二个参数代表 index 索引-->
<li v-for="(item, index) in dataList">姓名：{{item.name}} --- 年龄：{{item.age}} --- 索引：{{index}}</li>


```

way3：对象的遍历

```vue
obj1: {
name: 'qianguyihao',
age: '26',
gender: '男'
}
<!-- 括号里如果写两个参数：则第一个参数代表value，第二个参数代表key -->
<li v-for="(value,key) in obj1">值：{{value}} --- 键：{{key}} </li>

<h3>---分隔线---</h3>

<!-- 括号里如果写三个参数：则第一个参数代表value，第二个参数代表key，第三个参数代表index -->
<li v-for="(value,key,index) in obj1">值：{{value}} --- 键：{{key}} --- index：{{index}} </li>
```

way4：数字的遍历

```vue
<ul>
    <!-- 对象数组的遍历 -->
    <!-- 注意：如果使用 v-for 遍历数字的话，前面的 myCount 值从 1 开始算起 -->
    <li v-for="myCount in 10">这是第 {{myCount}}次循环</li>
</ul>
```

**注意**：在 Vue 2.2.0+ 版本里，当在**组件中**使用 v-for 时，key 属性是必须要加上的。

这样做是因为：每次 for 循环的时候，通过指定 key 来标示当前循环这一项的**唯一身份**。

> 当 Vue.js 用 v-for 正在更新已渲染过的元素列表时，它默认用 “**就地复用**” 策略。如果数据项的顺序被改变，Vue将**不是移动 DOM 元素来匹配数据项的顺序**， 而是**简单复用此处每个元素**，并且确保它在特定索引下显示已被渲染过的每个元素。

> 为了给 Vue 一个提示，**以便它能跟踪每个节点的身份，从而重用和重新排序现有元素**，你需要为每项提供一个唯一 key 属性。

key的类型只能是：string/number，而且要通过 v-bind 来指定。

**v-if：设置元素的显示与隐藏**

------

**作用**：根据表达式的值的真假条件，来决定是否渲染元素，如果为false则不渲染（达到隐藏元素的目的），如果为true则渲染。

在切换时，元素和它的数据绑定会被销毁并重建。

**v-show:设置元素显示和隐藏**

------

**作用**：根据表达式的真假条件，来切换元素的 display 属性。如果为false，则在元素上添加 `display:none`属性；否则移除`display:none`属性。

举例如下：（点击按钮时，切换和隐藏盒子）

我们直接把上一段代码中的`v-if`改成`v-show`就可以了：

`v-if`和`v-show`都能够实现对一个元素的隐藏和显示操作。

区别：

- v-if：每次都会重新添加/删除DOM元素
- v-show：每次不会重新进行DOM的添加/删除操作，只是在这个元素上添加/移除`style="display:none"`属性，表示节点的显示和隐藏。

优缺点：

- v-if：有较高的切换性能消耗。这个很好理解，毕竟每次都要进行dom的添加／删除操作。
- v-show：**有较高的初始渲染消耗**。也就是说，即使一开始`v-show="false"`，该节点也会被创建，只是隐藏起来了。而`v-if="false"`的节点，根本就不会被创建。

**总结**：

- 如果元素涉及到频繁的切换，最好不要使用 v-if, 而是推荐使用 v-show
- 如果元素可能永远也不会被显示出来被用户看到，则推荐使用 v-if

## 2.myTable实例

```vue
<template>
  <div class="app">
    <div dataSource>
      <input type="text" v-model="formData.id" />
      <input type="text" v-model="formData.name" />
      <button @click="addFunc">add</button>
      <input type="text" v-model="keyWords" />
    </div>
    <table class="myTabble">
      <th>ID</th>
      <th>name</th>
      <th>time</th>
      <th>operate</th>
      <tr v-for="item in search(keyWords)" :key="item.id">
        <td>{{ item.id }}</td>
        <td>{{ item.name }}</td>
        <td>{{ item.time }}</td>
        <td><a href="#" @click="deleteItem(item.id)">delete</a></td>
      </tr>
      <tr v-if="formList.length == 0">
        <td colspan="4">no data,add data first!</td>
      </tr>
    </table>
  </div>
</template>

<script>
export default {
  data() {
    return {
      formList: [
        { id: 1, name: "儒学", time: new Date() },
        { id: 2, name: "道教", time: new Date() },
        { id: 3, name: "王阳明心学", time: new Date() },
        { id: 4, name: "弗洛伊德", time: new Date() },
      ],
      formData: {
        id: 0,
        name: "",
      },
      keyWords: "",
    };
  },
  methods: {
    addFunc() {
      const formItem = {
        id: this.formData.id,
        name: this.formData.name,
        time: new Date(),
      };
      this.formList.push(formItem);
      this.formData.id = 0;
      this.formData.name = "";
    },
    deleteItem(id) {
      const selectItem = this.formList.findIndex(function (item) {
        return item.id == id;
      });
      this.formList.splice(selectItem, 1);
    },
    search(keyWords) {
      const filterList = this.formList.filter((item) => {
        if (item.name.includes(keyWords)) {
          return item;
        }
      });
      return filterList;
    },
  },
};
</script>

<style>
.myTabble {
  width: 800px;
  margin: 20px auto;
  border-collapse: collapse; /*这一行，不能少：表格的两边框合并为一条*/
}
.myTabble th {
  background: orange;
  color: white;
  font-size: 16px;
  border: 1px solid black;
  padding: 5px;
}

.myTabble tr td {
  text-align: center;
  font-size: 16px;
  padding: 5px;
  border: 1px solid black;
}
</style>

```

## 3.自定义过滤器

### 3.1 vue2过滤器

------

概念:vue允许我们自定义过滤器用于文本格式化，特别是在mustache插值表达式，v-bind表达式，过滤器被添加在JavaScript表达式的尾部，由管道符表示。

全局过滤器的使用，全局方法vue.filter()，接受两个参数：过滤器的名称，过滤器函数。

*题外话：看到日期格式化的例子中，getmont()+1的值才是真正的月份，这是因为getmonth返回的其实是索引(从09开始)*

### 3.2  时间格式化

------

ES6字符串新方法：`String.prototype.padStart(maxLength, fillString='')` 或 `String.prototype.padEnd(maxLength, fillString='')`来填充字符串。 `pad`在英文中指的是`补充`。

```VUE
<template>
  <div class="father">
    <!-- <p>{{ msg | msgFormat }}</p > -->
    <p>{{ datefmt(msg) }}</p >
</div>
</template>
<script>
// import { Vue } from 'vue-class-component';

// g表示全局匹配，fliter在vue3中已经弃用
// Vue.filter('msgFormat',function(msg) {
//       return msg.replace(/session/g,'snapshot')
//     })
//过滤函数可以有多个参数 function (myMsg, arg2, arg3)
//过滤中的管道符可以传递 {{msg | filter1 | filter2}}

export default {
  name:'app',
  data() {
    return {
      msg: new Date
    }
  },
  methods: { 
    datefmt(input) {
        let res;
        // const year=input.getFullYear();
        // const month =input.getMonth();
        // const day=input.getDate();

        //ES6写法
        const year=input.getFullYear().toString().padStart(2,'0');
        const month =input.getMonth().toString().padStart(2,'0');
        const day=input.getDate().toString().padStart(2,'0');

        res=year+'-'+month+'-'+day;
        return res;
      }
  }
}
</script>
<style>
  .num {
    background-color: green;
  }
  .first {
      height: 60px;
  }
</style>

```

## 4.自定义按键修饰符&自定义修饰指令

### 4.1 v-on的按键修饰符

------



```
    .enter
    .tab
    .delete (捕获 “删除” 和 “退格” 键)
    .esc
    .space
    .up
    .down
    .left
    .right
    1.0.8+版本：支持单字母的按键别名。
```

keyup指的是任何键位的抬起，.enter指的是ernter键的修饰符，两者结合： @keyup.enter      enter键抬起后。

F2键没有效果，因为F2键不是内置的按键修饰符，但是每个按键都有对应的按键码，F2对应113，于是便有 @keyup.113，还可以给键盘码定义别名。

```vue
 vue.config.keyCodes.f2=113;
```

### 4.2 自定义全局指令

------

vue.direvtive()   自定义全局指令：

```js
//自定义全局指令让文本自动获取焦点 v-focus；
//参数1：指令名称；
//参数二：一个对象，指令的相关函数，特定阶段执行相关的操作。
vue.directive('focus',{
bind:function(e1) {
},
inserted:function(e1) {
},
updated:function(e1) {
}
})

//e1:元素
//bind： 指令绑定到元素上时执行，此时元素还没有插入到DOM中，因此在bind里写focus不会生效，因为只有插入到DOM中才会有焦点；
//inserted: 元素插入到DOM中时执行；
//VNode： 当VNode更新时，执行updated。
//这三个函数也叫钩子函数
```

```vue
<template>
  <div class="app">
    <p>llllllllllllllllllllll</p>
    <input type="text" id="search" v-model="name" v-focus />
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "daijiubu",
    };
  },
  directive: {
    focus: {
      inserted: function (el) {
        el.focus();
      },
    },
  },
  methods: {
    test() {
    }
  }
};
</script>
<style>
#search {
  height: 150;
}
</style>

```

## 5.VUE实例的生命周期函数

beforeCreate：实例刚在内存中被创建出来，还没初始化好data和methods属性；

created：实例在内存中已创建ok，data和methods已创建ok，此时还没有编译模板，可以在这里进行ajax请求；

beforeMount：完成了模板的编译，还没有挂载到页面中；

mounted：编译好的模板已经挂碍到指定页面容器中，真实DOM被渲染了，可以操纵DOM了；

beforeUpdate：状态更新之前执行函数，data中的数据已是最新，但没重新开始渲染的DOM结点不是；

updated：实例更新完毕之后调用，数据和DOM结点都是最新的；

beforeDestroy：实例销毁前调用，此时实例仍然完全可用；可以这时清楚定时器或清除事件绑定；

destroyed：Vue实例销毁后调用，之后实例调用的所有东西都会被移除

```vue
<template>
  <div class="father">
<input type="button" value="modify flag" @click="mymethod">
<h3>{{ flag }}</h3>
</div>
</template>
<script>



export default {
  name:'app',
  data() {
    return {
      msg:'chaos progressively',
      flag:false
    }
  },
  beforeCreate:function() {
console.log('beforeCreate',this.msg)
  },
  created:function() {
console.log('created',this.msg)
  },
  beforeMount:function() {
console.log('beforeMount',this.msg)
  },
  mounted:function() {
console.log('mounted',this.msg)
  },
  methods: { 
    mymethod() {
      this.flag=true
    }
  },
  beforeUpdate:function() {
    console.log('beforeUpdate',this.msg)
    console.log('el show:',document.getElementById('h3').innerText())
    console.log('data',this.flag)
  },
  updated:function() {
    console.log('updated',this.msg)
    console.log('el show:',document.getElementById('h3').innerText())
    console.log('data',this.flag)
  }
}
</script>
<style>
  .num {
    background-color: green;
  }
  .first {
      height: 60px;
  }
</style>

```

## 6.Vue中的Ajax请求

 Vue-resource

高度集成的vue第三方包，vue.js文件向windows暴露了Vue这个关键词，vue-resource向vue挂载了this.http这个属性；

get、post

```vue
//get
this.$http.get("http://www.hikvison.com").then(function(response) {

})
//post
this.$http.post("http://www.hikvison.com",{},{emulateJSON:true}).then(function(response) {

})
```

## 7.vue组件

### 7.1 全局组件：使用Vue.extend方法定义组件，使用Vue.component方法注册组件

------



```vue
<template>
  <div class="app">
    <my-account></my-account>
  </div>
</template>
<!--写法三：-->
 <!-- <template id='my-account'> -->
  <!-- <div>
            <h2>登录页面</h2> -->
            <!-- <h3>注册页面</h3>
        </div> -->
  <!-- </template> -->

   <!--  <div id="app"> -->
        <!--  <account> </account> -->
      <!-- </div> -->
      
<script>


//写法一：
// const myAccount =Vue.extend({
//   template:'<div><h2>登录页面</h2> <h3>注册页面</h3></div>'
// })
// Vue.component('my-account', myAccount)

//写法二：一步到胃
// Vue.component('my-account', {
//   template:'<div><h2>登录页面</h2> <h3>注册页面</h3></div>'
// })

//写法三：
// Vue.component('account',{
//   template:'#account'
// })


export default {
  data() {
    return {
      formList: [],
      formData: {
        id: 0,
        name: "",
      },
      keyWords: "",
    };
  },
};
</script>

<style>

</style>

```

### 7.2 私有组件

------



```vue
<template id='loginTemp'>
  <div class="app">
  </div>
  </template>   
  <mylogin></mylogin> 
 

<script>
export default {
  data() {
    return {
      formList: [],
      formData: {
        id: 0,
        name: "",
      },
      keyWords: "",
    };
  },
  components: {
    mylogin:{
      template:'#loginTemp'
    }
  }
};
</script>
<style>
</style>

```

### 7.3 组件间传值

------

**父组件向子组件传值：props**
传值步骤：

在子组件的props属性中声明父亲传过来的数据；

定义子组件模板时，适用props中的属性；

父组件在引用子组件时，进行属性绑定；

子组件中，data和props的区别：

data可读可写，props可读，不可重新赋值

即可传递data中的属性也可传递方法

```vue
//传递data
<component1 v-bind:parent-msg="msg"></component1>
  props: ['parentMsg'],
//传递方法
 <component1 @parent-show='show'></component1>
methods: {
                show: function () { // 定义父组件的show方法
                    console.log('父组件提供的方法');
                }
            },
//只要在子组件中
  this.$emit('parent-show');
即可实现
```



**子组件向父组件传值**
在emit中作为含参传出即可

7.4 通过ref属性获取DOM元素

我们当然可以使用JS原生的做法（document.getElementById）或者 jQuery 来获取DOM，但是这种做法却在无形中操作了DOM，在Vue框架中并不推荐这种做法。

我们可以通过`ref`属性获取DOM元素。

**在Vue中，通过 ref 属性获取DOM元素**的步骤：

（1）第一步：在标签中给 DOM 元素设置 ref 属性。

```vue
    <h3 id="myH3" ref="myTitle"> 今天天气太好了</h3>
```



（2）第二步：通过 this.this.$refs.xxx 获取 DOM 元素

```vue
console.log(this.$refs.myTitle.innerText)
```

