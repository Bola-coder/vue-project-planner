<template>
  <h1>Project Planner</h1>
  <NavBar />
  <router-view />
</template>

<script>
import NavBar from "./components/NavBar.vue";
export default {
  components: { NavBar },
};
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 640px;
  margin: 0 auto;
  padding: 10px;
  background: #f2f2f2;
  color: #ddd;
}

#app h1 {
  text-align: center;
  font-size: 1.7rem;
}
</style>
