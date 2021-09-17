<template>
  <div class="home">
    <FilteredNav @filter="content = $event" :content="content" />
    <div v-if="projects.length">
      <div v-for="project in filteredProjects" :key="project.id">
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
import FilteredNav from "../components/FilteredNav.vue";
export default {
  name: "Home",
  components: { Project, FilteredNav },
  data() {
    return {
      url: "http://localhost:3000/projects",
      projects: [],
      content: "all",
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
  computed: {
    filteredProjects() {
      if (this.content === "completed") {
        return this.projects.filter((project) => project.complete);
      } else if (this.content === "ongoing") {
        return this.projects.filter((project) => !project.complete);
      } else {
        return this.projects;
      }
    },
  },
};
</script>

<style scoped>
.home {
  padding: 2px 10px;
}
</style>
