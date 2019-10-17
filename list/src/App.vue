<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png" />
    <HeaderTitle msg="The list of posts" />
    <ListPosts />
  </div>
</template>

<script>
import HeaderTitle from "./components/HeaderTitle.vue";
import ListPosts from "./components/ListPosts.vue";

export default {
  name: "app",
  components: {
    HeaderTitle,
    ListPosts
  }
};
</script>

<style>
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
