# My Vue Notes



## 1.VUE的系统指令

**插值表达式{{ msg}}**

------



```vue
{{ number + 1 }}

{{ ok ? 'YES' : 'NO' }}

{{ name == 'smyhvae' ? 'true' : 'false' }}

{{ message.split('').reverse().join('') }}
```

但只能包含单个表达式

**v-cloak**

------

`v-cloak`：保持和元素实例的关联，直到结束编译后自动消失。eg:{{name}}，当网速慢时页面会一直显示name，到加载完成后才会显示name对应的值，使用v-cloak后，未加载完成前会一直隐藏name直到加载完成再显示

**v-text**

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

**v-html**

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

**v-bind**

------

`v-bind`：用于绑定**属性**。

```vue
<img v-bind:src="imageSrc +'smyhvaeString'">

<div v-bind:style="{ fontSize: size + 'px' }"></div>
```

上方代码中，给属性加了 v-bind 之后，属性值里的整体内容是**表达式**，属性值里的`imageSrc`和`size`是Vue实例里面的**变量**。

也就是说， v-bind的属性值里，可以写合法的 js 表达式。

**v-on** 

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

**v-for的四种使用方式**

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

