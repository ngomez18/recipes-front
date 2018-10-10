<template>
  <div id="app">
    <Header />
    <Recipe />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Recipe from './components/Recipe.vue';

export default {
  name: 'app',
  components: {
    Header,
    Recipe
  },
};
</script>
