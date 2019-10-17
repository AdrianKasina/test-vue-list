<template>
  <transition name="modal">
    <div class="modal-mask">
      <div class="modal-wrapper">
        <div class="modal-container">
          <div class="modal-header">
            <input type="text" class="title-input" v-model="post.title" />
          </div>
          <div class="modal-body">
            <textarea type="text" rows="5" class="body-input" v-model="post.body"></textarea>
          </div>
          <button class="modal-default-button" @click="$emit('close'), upgrade(index)">save</button>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
import axios from "axios";

export default {
  name: "EditModal",
  props: {
    post: Object
  },
  methods: {
    upgrade: function(index) {
      axios
        .patch("https://jsonplaceholder.typicode.com/posts/" + index)
        .then(response => {
          alert(
            "HTTP status code from the server response: " + response.status
          );
        });
    }
  }
};
</script>

<style scoped>
.modal-mask {
  position: fixed;
  z-index: 9998;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: table;
  transition: opacity 0.3s ease;
}

.modal-wrapper {
  display: table-cell;
  vertical-align: middle;
}

.modal-container {
  width: 80%;
  margin: 0px auto;
  padding: 40px 30px 60px;
  background-color: #fff;
  border-radius: 2px;
  box-shadow: 0 2px 8px rgba(0, 0, 0, 0.33);
  transition: all 0.3s ease;
  font-family: Helvetica, Arial, sans-serif;
}

.modal-header h3 {
  margin-top: 0;
  color: #42b983;
}

.modal-body {
  margin: 20px 0;
}

.modal-default-button {
  float: right;
}

.modal-enter {
  opacity: 0;
}

.modal-leave-active {
  opacity: 0;
}

.modal-enter .modal-container,
.modal-leave-active .modal-container {
  -webkit-transform: scale(1.1);
  transform: scale(1.1);
}

.title-input {
  width: 90%;
  height: 2rem;
  font-size: 1rem;
  font-weight: 600;
  padding: 0 20px;
}

.body-input {
  font-family: Helvetica, Arial, sans-serif;
  width: 90%;
  font-size: 1rem;
  padding: 0 20px;
}

button {
  min-width: 64px;
  margin: 10px;
  padding: 8px;
  background: white;
  text-transform: uppercase;
  border: 1px solid #32ba54;
  color: #32ba54;
}
button:hover {
  background: rgba(194, 193, 202, 0.2);
}
</style>