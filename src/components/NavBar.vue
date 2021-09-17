<template>
  <nav>
    <router-link :to="{ name: 'Home' }">Home</router-link>
    <router-link :to="{ name: 'AddProject' }">Add New Project</router-link>
  </nav>
</template>

<script>
export default {};
</script>

<style>
nav {
  display: flex;
  justify-content: space-around;
  align-items: center;
  padding: 5px 20px;
}

nav a {
  text-decoration: none;
  font-size: 20px;
  color: #222;
  font-weight: bolder;
  padding: 6px 12px;
  margin-bottom: 5px;
}

nav a.router-link-exact-active {
  border-bottom: 2px solid green;
  padding-bottom: 5px;
}
</style>
