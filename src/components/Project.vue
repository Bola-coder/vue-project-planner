<template>
  <div class="project" :class="{ complete: project.complete }">
    <div class="action">
      <h3 class="project-name" @click="toggleDetails">{{ project.name }}</h3>
      <div class="icons">
        <span class="material-icons">
          edit
        </span>
        <span @click="deleteProject" class="material-icons">
          delete
        </span>
        <span @click="handleComplete" class="material-icons completed">
          done
        </span>
      </div>
    </div>
    <div class="detail">
      <p class="project-detail" v-if="showDetails">{{ project.details }}</p>
    </div>
  </div>
</template>

<script>
export default {
  props: ["project"],
  data() {
    return {
      showDetails: false,
      uri: ` http://localhost:3000/projects/${this.project.id}`,
    };
  },
  methods: {
    toggleDetails() {
      this.showDetails = !this.showDetails;
    },
    deleteProject() {
      fetch(this.uri, { method: "DELETE" })
        .then(() => this.$emit("delete", this.project.id))
        .catch((err) => console.log(err.message));
    },
    handleComplete() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify({ complete: !this.project.complete }),
      })
        .then(() => this.$emit("complete", this.project.id))
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style scoped>
.project {
  padding: 2px 7px;
  margin-bottom: 10px;
  border-left: 3px solid crimson;
  background: #fff;
}

.project.complete {
  border-color: green;
}

.project-name {
  cursor: pointer;
  color: rgba(0, 0, 0, 0.8);
  letter-spacing: 1px;
}

.project-name:hover {
  opacity: 70%;
}

.project-detail {
  line-height: 30px;
  color: #222;
}

.action {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.material-icons {
  padding: 10px;
  cursor: pointer;
  font-size: 1.5rem;
  color: #aaa;
  /* margin-left: 10px; */
}

.material-icons:hover {
  color: #555;
}
.project.complete .completed {
  color: green;
}
</style>
