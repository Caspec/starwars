<template>
  <div class="pagination mt-4 mb-4">
    <button 
      class="btn btn-warning me-2" 
      :disabled="currentPage === 1" 
      @click="onFirstPage">
      « First
    </button>

    <button 
      class="btn btn-warning me-2" 
      :disabled="currentPage === 1" 
      @click="onPreviousPage">
      ‹ Previous
    </button>

    <span class="mx-2">{{ currentPage }} / {{ totalPages }}</span>

    <button 
      class="btn btn-warning ms-2" 
      :disabled="currentPage === totalPages" 
      @click="onNextPage">
      Next ›
    </button>

    <button 
      class="btn btn-warning ms-2" 
      :disabled="currentPage === totalPages" 
      @click="onLastPage">
      Last »
    </button>
  </div>
</template>

<script>
export default {
  props: {
    currentPage: {
      type: Number,
      required: true
    },

    totalPages: {
      type: Number,
      required: true
    }
  },
  
  methods: {
    onFirstPage() {
      if (this.currentPage > 1) {
        this.$emit('update:currentPage', 1);
      }
    },

    onPreviousPage() {
      if (this.currentPage > 1) {
        this.$emit('update:currentPage', this.currentPage - 1);
      }
    },

    onNextPage() {
      if (this.currentPage < this.totalPages) {
        this.$emit('update:currentPage', this.currentPage + 1);
      }
    },

    onLastPage() {
      if (this.currentPage < this.totalPages) {
        this.$emit('update:currentPage', this.totalPages);
      }
    }
  }
}
</script>

<style scoped>
.pagination {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>
