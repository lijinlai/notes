本节来修改 store 中的数据。

### 添加 mutation

Vue 修改 store 中的数据，要通过对应模块的 mutations 来完成。

store/modules/comment.js

```js
const mutations = {
  addComment (state, comment) {
    state.all.push(comment)
  }
}

export default {
  state,
  mutations
}
```

### 呼叫 mutations

这个就是到对应组件中，由用户去触发了。

CommentBox.vue

```js
        this.$store.commit('addComment', comment)
        this.message = ''
      }
```

删除 this.comment.push 语句，改用 mutation 来修改 store 中存储的数据。

浏览器中，可以看到评论发送成功了。


### PostBody 中显示评论数量

PostBody.vue

```html
<template>
  <div class="post-body">
    <div class="comment-count">
      {{ commentCount }} 评论
    </div>
  </div>
</template>

<script>
  export default {
    computed: {
      commentCount() { return this.$store.state.comment.all.length }
    }
  }
</script>

<style>
  .post-body {
    position: relative;
  }

  .post-body .comment-count {
    position: absolute;
    bottom: 10px;
    right: 10px;
    border-bottom: 1px solid gray;
  }
</style>
```

模板中添加 commentCount 数据。

到 script 标签中，添加 computed 属性 commentCount ，从 store 中把数据读取出来。

下面再来添加点样式，利用 postion: relative 和 postion: absolute 配合，让评论数显示到 PostBody 区域的右下角。

浏览器中，看到每次提交评论，评论数都会变化。
