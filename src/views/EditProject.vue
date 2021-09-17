<template>
  <form @submit.prevent="updateProject">
    <label>Project title</label>
    <input type="text" v-model="title" class="title" required />
    <label>Project Details</label>
    <textarea type="text" v-model="details" class="detail" required></textarea>
    <div class="submit">
      <button>Update project</button>
    </div>
  </form></template
>

<script>
export default {
  props: ["id"],
  data() {
    return {
      title: "",
      details: "",
      uri: "http://localhost:3000/projects/" + this.id,
    };
  },
  mounted() {
    fetch(this.uri)
      .then((res) => res.json())
      .then((data) => {
        this.title = data.name;
        this.details = data.details;
      })
      .catch((err) => console.log(err.message));
  },

  methods: {
    updateProject() {
      fetch(this.uri, {
        method: "PATCH",
        headers: { "Content-type": "application/json" },
        body: JSON.stringify({ name: this.title, details: this.details }),
      })
        .then(() => {
          this.$router.push("/");
        })
        .catch((err) => consol.log(err));
    },
  },
};
</script>

<style></style>
