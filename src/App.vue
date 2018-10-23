<template>
  <div id="app">
    <Header v-bind:activeTab="activeTab"
            v-on:activateRecipes="activeTab=1"
            v-on:activateCreateRecipe="activeTab=2"/>
    <Recipes v-show="activeTab==1"/>
    <RecipeForm v-show="activeTab==2"/>
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

  data() {
    return {
      activeTab: 1
    }
  }
};
</script>
