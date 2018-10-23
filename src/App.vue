<template>
  <div id="app">
    <Header v-bind:activeTab="activeTab"
            v-on:activateRecipes="viewRecipes"
            v-on:activateCreateRecipe="createRecipe"/>
    <Recipes v-show="showList"/>
    <RecipeForm v-show="!showList"/>
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
      activeTab: 1,
      showList: true,
    };
  },

  methods: {
    viewRecipes() {
      this.showList = true;
      this.activeTab = 1;
    },
    editRecipe() {
      this.showList = false;
      this.activeTab = 1;
    },
    createRecipe() {
      this.showList = false;
      this.activeTab = 2;
    },
  },
};
</script>
