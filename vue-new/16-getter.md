# 使用 getter 简化代码


PostBody.vue 中


```js
      commentCount() { 
        return this.$store.state.comment.all.filter(
          t => t.post === this.postId
        ).length 
      },
```

浏览器中，可以看到评论数量显示正确了。


### 代码移动到 getter 


modules/comment.js

```js
const getters = {
  getComments: (state) => (id) => {
    return state.all.filter(t => t.post === id)
  }
}
export default {
  state,
  mutations,
  actions,
  getters
}
```

CommentBox.vue

```js
      comments() { 
        return this.$store.getters.getComments(this.postId)
      },
```


PostBody.vue

```js
      commentCount() { 
        return this.$store.getters.getComments(this.postId).length 
      },
```
