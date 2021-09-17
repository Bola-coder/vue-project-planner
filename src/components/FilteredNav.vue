<template>
  <nav class="filtered-nav">
    <button @click="updateFilter('all')" :class="{ active: content === 'all' }">
      All
    </button>
    <button
      @click="updateFilter('completed')"
      :class="{ active: content === 'completed' }"
    >
      Completed
    </button>
    <button
      @click="updateFilter('ongoing')"
      :class="{ active: content === 'ongoing' }"
    >
      Ongoing
    </button>
  </nav>
</template>

<script>
export default {
  props: ["content"],
  methods: {
    updateFilter(arg) {
      this.$emit("filter", arg);
    },
  },
};
</script>

<style>
.filtered-nav button {
  /* padding: 10px 20px; */
  font-size: 12px;
  text-transform: uppercase;
  letter-spacing: 1px;
  font-weight: bold;
  margin-right: 5px;
  outline: none;
  background: none;
  border: none;
  color: #bbb;
  cursor: pointer;
}

.filtered-nav button.active {
  color: #555;
}
</style>
