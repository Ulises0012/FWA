<template>
    <div class="character-details">
      <p>Nivel: {{ character.level }}</p>
      <p>Clase: {{ character.class }}</p>
      <button @click="showMoreDetails">Ver más detalles</button>
    </div>
  </template>
  
  <script>
  export default {
    name: 'CharacterDetails',
    props: {
      character: {
        type: Object,
        required: true
      }
    },
    methods: {
      showMoreDetails() {
        this.$emit('show-details', this.character.id);
      }
    }
  }
  </script>
  
  <style scoped>
  .character-details {
    margin-top: 15px;
    padding-top: 15px;
    border-top: 1px solid #eee;
  }
  
  button {
    background-color: #007bff;
    color: white;
    border: none;
    padding: 8px 16px;
    border-radius: 4px;
    cursor: pointer;
    transition: background-color 0.2s;
  }
  
  button:hover {
    background-color: #0056b3;
  }
  
  p {
    margin: 5px 0;
    color: #666;
  }
  </style>