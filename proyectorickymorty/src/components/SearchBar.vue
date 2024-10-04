<template>
    <div class="search-bar">
      <input 
        type="text" 
        v-model="searchTerm" 
        placeholder="Buscar personaje..."
        @input="emitSearch"
      >
    </div>
  </template>
  
  <script>
  export default {
    name: 'SearchBar',
    data() {
      return {
        searchTerm: ''
      }
    },
    methods: {
      emitSearch() {
        this.$emit('search', this.searchTerm);
      }
    }
  }
  </script>
  
  <style scoped>
  .search-bar input {
    width: 100%;
    padding: 8px;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-size: 1rem;
  }
  
  .search-bar input:focus {
    outline: none;
    border-color: #007bff;
    box-shadow: 0 0 0 2px rgba(0,123,255,0.25);
  }
  </style>