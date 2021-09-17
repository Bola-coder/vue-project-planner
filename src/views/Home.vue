<template>
  <div class="home">
    <div v-if="projects.length">
      <div v-for="project in projects" :key="project.id">
        <Project
          :project="project"
          @delete="handleDelete"
          @complete="handleComplete"
        />
      </div>
    </div>
    <div v-else style="text-align: center; color: black">
      Loading projects.....
    </div>
  </div>
</template>

<script>
import Project from "../components/Project";
export default {
  name: "Home",
  components: { Project },
  data() {
    return {
      url: "http://localhost:3000/projects",
      projects: [],
    };
  },
  mounted() {
    fetch(this.url)
      .then((res) => res.json())
      .then((data) => {
        this.projects = data;
      })
      .catch((err) => console.log(err.message));
  },
  methods: {
    handleDelete(id) {
      this.projects = this.projects.filter((project) => project.id !== id);
    },
    handleComplete(id) {
      let foundProject = this.projects.find((project) => project.id === id);
      foundProject.complete = !foundProject.complete;
    },
  },
};
</script>

<style scoped>
.home {
  padding: 10px 18px;
}
</style>
