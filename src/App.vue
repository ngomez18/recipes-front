<template>
  <div id="app">
    <Header v-bind:activeTab="activeTab"
            v-on:activateRecipes="viewRecipes"
            v-on:activateCreateRecipe="createRecipe"/>
    <Recipes v-show="showList"
            v-bind:recipes="recipes"
            v-on:deleteRecipe="deleteRecipe"
            v-on:editRecipe="editRecipe" />
    <RecipeForm v-show="!showList"
                v-bind:recipe="activeRecipe"
                v-bind:editMode="editMode"
                v-on:cancel="viewRecipes"
                v-on:save="saveRecipe" />
  </div>
</template>

<script>
import axios from 'axios';
import swal from 'sweetalert';
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
      activeRecipe: {
        name: '',
        description: '',
        image: '',
        requiredTime: '',
        difficulty: '',
        servings: '',
        steps: '',
        ingredients: [],
      },
      recipes: [],
      editMode: false,
    };
  },

  mounted() {
    this.fetchRecipes();
  },

  methods: {
    viewRecipes() {
      this.showList = true;
      this.activeTab = 1;
    },
    editRecipe(recipe) {
      this.showList = false;
      this.editMode = true;
      this.activeTab = 1;
      this.activeRecipe = recipe;
    },
    createRecipe() {
      this.showList = false;
      this.activeTab = 2;
      this.activeRecipe = {
        name: '',
        description: '',
        image: '',
        requiredTime: '',
        difficulty: '',
        servings: '',
        steps: '',
        ingredients: [],
      };
    },
    fetchRecipes() {
      axios.get('https://recipes-api-go.herokuapp.com/api/recipes')
        .then((response) => { this.recipes = response.data; })
        .catch(error => console.log(error));
    },
    saveRecipe(recipe) {
      if (recipe.ID) {
        // Update recipe
        axios.put('https://recipes-api-go.herokuapp.com/api/recipe', recipe)
          .then((response) => {
            if (response.status === 200) {
              swal({ icon: 'success' });
              this.viewRecipes();
            }
          })
          .catch((error) => {
            swal({
              text: 'Something went wrong!',
              icon: 'error',
            });
            console.log(error);
          });
      } else {
        // Create recipe
        axios.post('https://recipes-api-go.herokuapp.com/api/recipe', recipe)
          .then((response) => {
            if (response.status === 201) {
              swal({ icon: 'success' });
              const newRecipe = response.data;
              this.recipes.push(newRecipe);
              this.viewRecipes();
            }
          })
          .catch((error) => {
            swal({
              text: 'Something went wrong!',
              icon: 'error',
            });
            console.log(error);
          });
      }
    },
    deleteRecipe(id) {
      const vm = this; // View Model
      axios.delete(`https://recipes-api-go.herokuapp.com/api/recipe/${id}`)
        .then((response) => {
          if (response.status === 200) {
            swal({ icon: 'success' });
            vm.recipes = vm.recipes.filter(r => r.ID !== id);
          }
        })
        .catch((error) => {
          swal({
            text: 'Something went wrong!',
            icon: 'error',
          });
          console.log(error);
        });
    },
  },
};
</script>
