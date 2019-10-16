<template>
  <div id="posts">
    <ul>
      <li v-for="post in posts" :key="post.id">
        <h3>{{ post.title }}</h3>
        <p>{{ post.body }}</p>
      </li>
    </ul>
    <!-- <ul>
      <li v-for="item in items" :key="item.id">{{ item }}</li>
    </ul>-->
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "ListPosts",
  data() {
    return {
      posts: null
    };
  },
  mounted() {
    axios
      .get("https://jsonplaceholder.typicode.com/posts")
      .then(response => (this.posts = response.data))
      .catch(error => console.log(error)); // eslint-disable-line no-console
  }
};
</script>

<style scoped>
h3 {
  margin: 40px 0 0;
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