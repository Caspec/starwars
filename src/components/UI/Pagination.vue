<template>
    <div class="pagination mt-4 mb-4">
      <button 
        class="btn btn-warning" 
        :disabled="currentPage === 1" 
        @click="onPreviousPage">
        Previous
      </button>
      <span class="mx-2">{{ currentPage }} / {{ totalPages }}</span>
      <button 
        class="btn btn-warning" 
        :disabled="currentPage === totalPages" 
        @click="onNextPage">
        Next
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
      onPreviousPage() {
        if (this.currentPage > 1) {
          this.$emit('update:currentPage', this.currentPage - 1);
        }
      },
      
      onNextPage() {
        if (this.currentPage < this.totalPages) {
          this.$emit('update:currentPage', this.currentPage + 1);
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
  