<template>
  <div id="app">
    <header-component />
    <main>
      <character-list />
    </main>
    <footer-component />
  </div>
</template>

<script>
import CharacterList from './components/CharacterList.vue';
import HeaderComponent from './components/HeaderComponent.vue';
import FooterComponent from './components/FooterComponent.vue';

export default {
  name: 'App',
  components: {
    CharacterList,
    HeaderComponent,
    FooterComponent
  }
}
</script>

<style>
#app {
  font-family: Arial, sans-serif;
  background-color: #f5f5f5;
  min-height: 100vh;
}

main {
  padding: 20px;
  max-width: 1200px;
  margin: 0 auto;
}
</style>