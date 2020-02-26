<template>
  <div id="app">
    <To_do_list />
    <!-- <SearchPhoto /> -->
  </div>
</template>

<script>
import To_do_list from "./components/To_do_list.vue";
// import SearchPhoto from "./components/SearchPhoto.vue";

export default {
  name: "app",
  components: {
    To_do_list
    // SearchPhoto
  }
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}
#app {
  max-width: 500px;
  height: 100vh;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  font-family: "Indie Flower";
  text-align: center;
  color: #2c3e50;
}
</style>
