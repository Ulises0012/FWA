<template>
    <header class="app-header">
      <div class="header-content">
        <h1>Rick and Morty</h1>
        
      </div>
    </header>
  </template>
  
  <script>
  export default {
    name: 'HeaderComponent'
  }
  </script>
  
  <style scoped>
  .app-header {
    background-color: #97ce4c;
    padding: 2rem;
    box-shadow: 0 2px 4px rgba(0,0,0,0.1);
    text-align: center;
  }
  
  .header-content {
    max-width: 1200px;
    margin: 0 auto;
  }
  
  h1 {
    margin: 0;
    color: #2c2c2c;
    font-size: 3rem;
    font-weight: bold;
    text-transform: uppercase;
    text-shadow: 2px 2px 4px rgba(0,0,0,0.2);
  }
  
  .subtitle {
    color: #2c2c2c;
    font-size: 1.5rem;
    margin-top: 0.5rem;
    font-weight: 500;
  }
  
  .header-image {
    margin-top: 1rem;
  }
  
  .header-image img {
    max-width: 300px;
    height: auto;
  }
  
  @media (max-width: 768px) {
    h1 {
      font-size: 2rem;
    }
  
    .subtitle {
      font-size: 1.2rem;
    }
  
    .header-image img {
      max-width: 200px;
    }
  }
  </style>