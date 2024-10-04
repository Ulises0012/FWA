<template>
    <div class="character-container">
      <div class="filters">
        <input 
          v-model="searchQuery"
          @input="handleSearch"
          type="text"
          placeholder="Buscar por nombre..."
          class="search-input"
        />
        <select v-model="selectedStatus" @change="handleFilterChange">
          <option value="all">Todos</option>
          <option value="Alive">Vivo</option>
          <option value="Dead">Muerto</option>
          <option value="unknown">Desconocido</option>
        </select>
      </div>
  
      <div class="character-grid">
        <CharacterCard 
          v-for="character in characters" 
          :key="character.id"
          :character="character"
        />
      </div>
  
      <div class="pagination">
        <button 
          :disabled="currentPage === 1" 
          @click="changePage(currentPage - 1)"
        >
          Anterior
        </button>
        <span>Página {{ currentPage }} de {{ totalPages }}</span>
        <button 
          :disabled="currentPage === totalPages" 
          @click="changePage(currentPage + 1)"
        >
          Siguiente
        </button>
      </div>
    </div>
  </template>
  
  <script>
  import CharacterCard from './CharacterCard.vue';
  import axios from 'axios';
  
  export default {
    name: 'CharacterList',
    components: {
      CharacterCard
    },
    data() {
      return {
        characters: [],
        currentPage: 1,
        totalPages: 0,
        selectedStatus: 'all',
        searchQuery: '',
        searchTimeout: null
      }
    },
    created() {
      this.fetchCharacters();
    },
    methods: {
      async fetchCharacters() {
        try {
          let url = `https://rickandmortyapi.com/api/character/?page=${this.currentPage}`;
          
          // Añadir filtros a la URL
          const filters = [];
          if (this.selectedStatus !== 'all') {
            filters.push(`status=${this.selectedStatus}`);
          }
          if (this.searchQuery) {
            filters.push(`name=${this.searchQuery}`);
          }
          
          if (filters.length > 0) {
            url += '&' + filters.join('&');
          }
  
          const response = await axios.get(url);
          this.characters = response.data.results;
          this.totalPages = response.data.info.pages;
        } catch (error) {
          console.error('Error:', error);
          this.characters = [];
          this.totalPages = 0;
        }
      },
      
      changePage(newPage) {
        this.currentPage = newPage;
        this.fetchCharacters();
      },
  
      handleSearch() {
        // Debounce para la búsqueda
        if (this.searchTimeout) clearTimeout(this.searchTimeout);
        this.searchTimeout = setTimeout(() => {
          this.currentPage = 1;
          this.fetchCharacters();
        }, 300);
      },
  
      handleFilterChange() {
        this.currentPage = 1;
        this.fetchCharacters();
      }
    }
  }
  </script>
  
  <style scoped>
  .character-container {
    padding: 20px;
  }
  
  .filters {
    margin-bottom: 20px;
    display: flex;
    gap: 10px;
  }
  
  .search-input {
    padding: 8px 16px;
    font-size: 1rem;
    border-radius: 4px;
    border: 1px solid #ddd;
    flex: 1;
    max-width: 300px;
  }
  
  select {
    padding: 8px 16px;
    font-size: 1rem;
    border-radius: 4px;
    border: 1px solid #ddd;
  }
  
  .character-grid {
    display: grid;
    grid-template-columns: repeat(auto-fill, minmax(300px, 1fr));
    gap: 20px;
    margin-bottom: 20px;
  }
  
  .pagination {
    display: flex;
    justify-content: center;
    align-items: center;
    gap: 20px;
    margin-top: 20px;
  }
  
  .pagination button {
    padding: 8px 16px;
    font-size: 1rem;
    border-radius: 4px;
    border: none;
    background-color: #007bff;
    color: white;
    cursor: pointer;
  }
  
  .pagination button:disabled {
    background-color: #cccccc;
    cursor: not-allowed;
  }
  
  .pagination span {
    font-size: 1rem;
  }
  </style>