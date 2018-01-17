# 添加文章数据


### 读 API 数据

App.vue

```js
  created() {
    this.$store.dispatch({ type: 'loadPosts' })
  }
```

发出加载所有文章的 action 。


modules/post.js

```js
import axios from 'axios'

const state = {
  all: []
}

const mutations = {
  loadPosts(state, posts) {
    state.all = posts
  }
}

const actions = {
  loadPosts({ commit }) {
    const uri = 'http://localhost:3008/posts'
    axios.get(uri).then(
      res => {
        const posts = res.data
        commit('loadPosts', posts)
      }
    )
  }
}

export default {
  state,
  mutations,
  actions
}
```

添加 post.js 模块，里面的思路和 comment 模块非常类似，主要实现了 loadPosts ，也就是加载评论功能。

首先添加 action 。

再来添加 mutation。

最后把 state ，action 和 mutation 一起导出。

store/index.js

```js
import post from './modules/post'

export default new Vuex.Store({
  modules: {
    comment,
    post
  }
})
```

store 文件中加载一下 post 模块。

Home.vue

```html
<template>
  <div class="home">
    {{ posts }}
  </div>
</template>

<script>
export default {
  name: 'Home',
  computed: {
    posts () {
      return this.$store.state.post.all
    }
  }
}
</script>
```

Home.vue 里面拿一下 store 的数据。

添加一个计算属性。posts ，拿到 store 中的 post.all 数据。

模板中显示出 posts 数据。

浏览器中，可以看到 posts 数组显示出来了。

### 显示列表

```html
    <ul>
      <li :key="post.id" v-for="post in posts">
        <router-link :to="'post/' + post.id">{{ post.title }}</router-link>
      </li>
    </ul>
```


浏览器中，可以看到一个文章列表了。点开每一项都能看到文章页面。


### 显示文章标题

PostBody.vue

```js
<template>
  <div class="post-body">
    <h1>{{ post.title }}</h1>
</template>

<script>
    computed: {
      post() {
        return this.$store.state.post.all.find(
          t => t.id === this.postId
        )
      }
    }
</script>
```

显示一篇文章的标题。
