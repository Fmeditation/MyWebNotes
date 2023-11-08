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