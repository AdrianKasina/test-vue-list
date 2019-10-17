<template>
  <div id="posts">
    <ul>
      <li v-for="(post, index) in posts" :key="post.id">
        <h3>{{ post.title }}</h3>
        <p>{{ post.body }}</p>
        <button class="edit">Edit</button>
        <button class="delete" @click="deletePost(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "ListPosts",
  data() {
    return {
      posts: []
    };
  },
  created() {
    axios
      .get("https://jsonplaceholder.typicode.com/posts")
      .then(response => (this.posts = response.data))
      .catch(error => console.log(error)); // eslint-disable-line no-console
  },

  methods: {
    deletePost: function(index) {
      axios
        .delete("https://jsonplaceholder.typicode.com/posts/" + index)
        .then(() => {
          this.posts.splice(index, 1);
        });
    }
  }
};
</script>

<style scoped>
h3 {
  margin: 30px 0 0;
}
ul {
  list-style-type: none;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
}

li {
  width: 80%;
  padding: 0 25px 15px;
  border: 1px solid #f37061;
  margin: 10px 0;
}
a {
  color: #42b983;
}

button {
  min-width: 64px;
  margin: 10px;
  padding: 8px;
  background: white;
  text-transform: uppercase;
}

.edit {
  border: 1px solid #32ba54;
  color: #32ba54;
}

.delete {
  border: 1px solid #de4710;
  color: #de4710;
}
</style>