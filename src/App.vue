<template>
<div id='app'>
  <h1>Bob Loblaw's Law Blog</h1>
  <button @click='switcheroo'>Switch</button>
  <section v-if='show_form'>
    <h3>Create New Blog Post</h3>
    <form @submit.prevent='submitNewPost'>
      <textarea v-model='newPost' name="" id="" cols="30" rows="10"></textarea><br>
      Author: <input type="text" v-model='author'><br>
      <button >Submit new post</button>
    </form>
  </section>
  <section v-else>
    <h3>List of Blog Posts</h3>
    <list :posts='posts' :removePost = 'removePost'></list>
    <!-- colon at beginning binds  -->
  </section>

</div>
</template>

<script>
import List from "./Components/List";
export default {
  components: {
    list: List
  },
  data() {
    return {
      newPost: "",
      author: "",
      posts: [],
      id: 0,
      show_form: true
    };
  },
  methods: {
    submitNewPost() {
      this.id++;
      let newPost = {
        id: this.id,
        content: this.newPost,
        author: this.author,
        timeStamp: new Date()
      };
      this.posts.push(newPost);
      this.newPost = "";
      this.author = "";
      this.switcheroo();
    },
    switcheroo() {
      this.show_form = !this.show_form;
    },
    removePost(id) {
      this.posts = this.posts.filter(post => {
        return post.id !== id;
      });
    }
  }
};
</script>

<style scoped>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

h1,
h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}
</style>
