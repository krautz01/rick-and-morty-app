<template>
  <div class="filters">
    <input v-model="name" placeholder="Name" />
    <select v-model="status">
      <option value="">All</option>
      <option value="alive">Alive</option>
      <option value="dead">Dead</option>
      <option value="unknown">Unknown</option>
    </select>
    <button @click="applyFilters">Apply</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      name: "",
      status: "",
    };
  },
  emits: ["applyFilters"],
  methods: {
    applyFilters() {
      this.$emit("applyFilters", { name: this.name, status: this.status });
    },
  },
};
</script>
