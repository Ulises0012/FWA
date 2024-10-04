<template>
    <div class="character-card">
      <img :src="character.image" :alt="character.name">
      <div class="character-info">
        <h3>{{ character.name }}</h3>
        <div class="status">
          <span 
            class="status-indicator"
            :class="statusClass"
          ></span>
          {{ character.status }} - {{ character.species }}
        </div>
        <div class="details">
          <p><strong>Origen:</strong> {{ character.origin.name }}</p>
          <p><strong>Ubicación:</strong> {{ character.location.name }}</p>
        </div>
      </div>
    </div>
  </template>
  
  <script>
  export default {
    name: 'CharacterCard',
    props: {
      character: {
        type: Object,
        required: true
      }
    },
    computed: {
      statusClass() {
        return {
          'alive': this.character.status === 'Alive',
          'dead': this.character.status === 'Dead',
          'unknown': this.character.status === 'unknown'
        }
      }
    }
  }
  </script>
  
  <style scoped>
  .character-card {
    border: 1px solid #ddd;
    border-radius: 8px;
    overflow: hidden;
    background: white;
    transition: transform 0.2s;
  }
  
  .character-card:hover {
    transform: translateY(-5px);
    box-shadow: 0 4px 8px rgba(0,0,0,0.1);
  }
  
  .character-card img {
    width: 100%;
    height: 200px;
    object-fit: cover;
  }
  
  .character-info {
    padding: 15px;
  }
  
  h3 {
    margin: 0 0 10px 0;
    color: #333;
  }
  
  .status {
    display: flex;
    align-items: center;
    margin-bottom: 10px;
  }
  
  .status-indicator {
    width: 10px;
    height: 10px;
    border-radius: 50%;
    margin-right: 8px;
  }
  
  .alive {
    background-color: #55cc44;
  }
  
  .dead {
    background-color: #d63d2e;
  }
  
  .unknown {
    background-color: #9e9e9e;
  }
  
  .details {
    margin-top: 10px;
  }
  
  .details p {
    margin: 5px 0;
    color: #666;
  }
  </style>