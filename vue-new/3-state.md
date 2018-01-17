# 组件内使用 state 

显示两条评论在页面上。数据通过组件内的 state 来提供。参考：https://cn.vuejs.org/v2/guide/list.html 。

### 添加 state

CommentBox.vue

```js
<template>
  <div class="comment-box">
    {{ comment }}
  </div>
</template>

<script>
  export default {
    name: 'CommentBox',
    data: () => ({
      comment: 'my comment'
    })
  }
</script>
```

到 CommentBox.vue 中，如果有一个 state 叫 comment ，就可以用双大括号的语法来使用它。

到 script 标签内，添加 data 这个属性，vue 组件中把 state ，通常就叫 data 了。后面注意，不能直接写一个对象，而[要写一个函数](https://cn.vuejs.org/v2/guide/components.html#data-%E5%BF%85%E9%A1%BB%E6%98%AF%E5%87%BD%E6%95%B0)，让他的返回值是一个对象，对象中可以写 state 变量了，我们这里需要的是 comment ，值是 'my comment' 字符串。

浏览器中，可以看到 state 显示到了页面上。


### 显示一个评论列表


CommentBox.vue

```js
<template>
  <div class="comment-box">
    <div v-for="comment in comments">
      {{ comment }}
    </div>
  </div>
</template>

<script>
  export default {
    data: () => ({
      comments: [
        '评论1',
        '评论2'
      ]
    })
  }
</script>
```

首先添加 comments 数据，是一个数组，里面有两个字符串。

到模板文件中，这里不是一个 js 环境，所以不能用 map 等各种 js 方法来显示列表。而要用 vue 模板提供的一种专门的智能机制，也就是[指令](https://cn.vuejs.org/v2/guide/syntax.html#指令)。一个指令就是一个用 v- 打头的特殊属性。我们这里使用 v-for ，等号后面是一个字符串，里面写 comment in commments 实现循环。这样 comment 显示到 div 中。同时 vue 规定，v-for 不能用在顶级组件中，所以要把外部再包裹一层 div ，同时把 class 名移动到外层 div 保证样式应用正确。

### 添加 v-bind:key 

列表的每一个元素都要添加一个独立的 key 。

CommentBox 中，


```js
  <div v-bind:key="comment.id" v-for="comment in comments">
    {{ comment.body }}
  </div>

      comments: [
        {
          id: '1',
          body: '评论1'
        },
        {
          id: '2',
          body: '评论2'
        }
      ]   
```

CommentBox.vue 中，把 comments 数据改一下，添加 id 进来，把评论主体内容保存为 body 属性的值。

到模板中，添加 v-bind 即可。

### 逆序显示评论

Vue 推荐用[计算属性](https://vuejs.org/v2/guide/computed.html)来进行对已有 data 的计算，而不要把计算过程直接写到模板中。

CommentBox.vue

```js
<template>
    <div v-bind:key="comment.id" v-for="comment in reversedComments">
</template>

<script>
  export default {
    computed: {
      reversedComments: function () { return this.comments.reverse() }
    }
  }
</script>
```

script 标签中，添加 computed 一项，值是一个对象，里面可以添加多个计算属性，每个计算属性的都要通过函数返回值的形式来提供。而且这里的函数必须是 ES5 的函数，不然会导致 this 未定义错误。

直接对 comments 进行 reverse() 操作，违背了不变性原则，但是这里我们先写成这样，下一节提交评论的时候，就会看到这个做法的弊端了。
