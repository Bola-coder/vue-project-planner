<template>
  <nav>
    <router-link to="/">Home</router-link>
    <router-link to="/add">Add New Project</router-link>
  </nav>
</template>

<script>
export default {};
</script>

<style>
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
}

nav a {
  text-decoration: none;
  font-size: 20px;
  color: #222;
  font-weight: bolder;
  padding: 6px 12px;
  margin-bottom: 20px;
}

nav a.router-link-exact-active {
  background: #aaa;
  border-radius: 10px;
}
</style>
