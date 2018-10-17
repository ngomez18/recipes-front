<template>
  <div id="app">
    <Header />
    <Recipes />
    <RecipeForm />
  </div>
</template>

<script>
import Header from './components/Header.vue';
import Recipes from './components/Recipes.vue';
import RecipeForm from './components/RecipeForm.vue';

export default {
  name: 'app',
  components: {
    Header,
    Recipes,
    RecipeForm,
  },
};
</script>
