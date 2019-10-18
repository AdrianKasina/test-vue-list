<template>
  <div id="posts">
    <Modal v-if="showModal" @close="showModal = false" :post="currentPost"></Modal>
    <ul>
      <li v-for="(post, index) in posts" :key="post.id">
        <h3>{{ post.title }}</h3>
        <p>{{ post.body }}</p>
        <button class="edit" id="show-modal" @click="showModal = true, currentPost = post">Edit</button>
        <button class="delete" @click="deletePost(index)">Delete</button>
      </li>
    </ul>
  </div>
</template>

<script>
import axios from "axios";
import Modal from "./ViewPostModal.vue";

export default {
  name: "PostsList",
  components: {
    Modal
  },

  data() {
    return {
      posts: [],
      showModal: false,
      currentPost: false
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
        .then(response => {
          this.posts.splice(index, 1);
          alert(
            "HTTP status code from the server response: " + response.status
          );
        });
    }
    // onClickEdit: function(index) {
    //   console.log(index); // eslint-disable-line no-console
    // }
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
  padding: 0;
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

button:hover {
  background: rgba(194, 193, 202, 0.2);
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