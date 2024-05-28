<template>
  <div class="pagination">
    <button @click="prevPage" :disabled="currentPage === 1">Previous</button>
    <span>Page {{ currentPage }}</span>
    <button @click="nextPage" :disabled="currentPage === totalPages">
      Next
    </button>
  </div>
</template>

<script>
export default {
  name: "CharacterPagination",
  props: {
    currentPage: Number,
    totalPages: Number,
  },
  emits: ["pageChange"],
  methods: {
    nextPage() {
      if (this.currentPage < this.totalPages) {
        this.$emit("pageChange", this.currentPage + 1);
      }
    },
    prevPage() {
      if (this.currentPage > 1) {
        this.$emit("pageChange", this.currentPage - 1);
      }
    },
  },
};
</script>
