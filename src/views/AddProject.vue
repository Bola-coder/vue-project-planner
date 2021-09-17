<template>
  <form @submit.prevent="handleSubmit">
    <label>Project title</label>
    <input type="text" v-model="title" class="title" required />
    <label>Project Details</label>
    <textarea type="text" v-model="details" class="detail" required></textarea>
    <div class="submit">
      <button>Add project</button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      title: "",
      details: "",
      url: "http://localhost:3000/projects",
    };
  },
  methods: {
    handleSubmit() {
      let project = {
        name: this.title,
        details: this.details,
        complete: false,
      };
      fetch(this.url, {
        method: "POST",
        headers: { "Content-Type": "application/json" },
        body: JSON.stringify(project),
      })
        .then(() => {
          this.$router.push("/");
        })
        .catch((err) => console.log(err.message));
    },
  },
};
</script>

<style>
form {
  max-width: 420px;
  margin: 30px auto;
  background: #fff;
  text-align: left;
  padding: 40px;
  border-radius: 10px;
}

label {
  color: #aaa;
  display: inline-block;
  margin: 25px 0 15px;
  font-size: 0.7em;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
}

input,
textarea {
  display: block;
  padding: 10px 6px;
  width: 100%;
  box-sizing: border-box;
  border: none;
  border-bottom: 1px solid #ddd;
}
textarea {
  border: 2px solid #ddd;
  height: 130px;
}

input:focus,
textarea:focus {
  opacity: 0.5;
}

button {
  background: #0b6dff;
  border: 0;
  padding: 10px 20px;
  margin-top: 40px;
  color: #fff;
  border-radius: 20px;
}
.submit {
  text-align: right;
}
</style>
