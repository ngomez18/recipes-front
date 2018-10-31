<template>
  <div id="app">
    <Header v-bind:activeTab="activeTab"
            v-on:activateRecipes="viewRecipes"
            v-on:activateCreateRecipe="createRecipe"/>
    <div v-if="loading" class="lds-dual-ring"></div>
    <Recipes v-show="showList && !loading"
            v-bind:recipes="recipes"
            v-on:deleteRecipe="deleteRecipe"
            v-on:editRecipe="editRecipe" />
    <RecipeForm v-show="!showList && !loading"
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

const emptyRecipe = {
  name: '',
  description: '',
  image: '',
  requiredTime: '',
  difficulty: '',
  servings: '',
  steps: '',
  ingredients: [
    {
      name: '',
      type: '',
    },
  ],
};

export default {
  name: 'app',
  components: {
    Header,
    Recipes,
    RecipeForm,
  },

  data() {
    return {
      loading: true,
      activeTab: 1,
      showList: true,
      activeRecipe: emptyRecipe,
      recipes: [],
      editMode: false,
    };
  },

  mounted() {
    this.fetchRecipes();
  },

  methods: {
    viewRecipes() {
      this.fetchRecipes();
      this.showList = true;
      this.activeTab = 1;
    },
    createRecipe() {
      this.showList = false;
      this.editMode = false;
      this.activeTab = 2;
      this.activeRecipe = emptyRecipe;
    },
    editRecipe(recipe) {
      this.showList = false;
      this.editMode = true;
      this.activeTab = 1;
      this.activeRecipe = recipe;
    },
    fetchRecipes() {
      this.loading = true;
      axios.get('https://recipes-api-go.herokuapp.com/api/recipes')
        .then((response) => {
          this.recipes = response.data;
          this.loading = false;
        })
        .catch((error) => {
          console.log(error);
          this.loading = false;
        });
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

<style lang="scss" scoped>
.lds-dual-ring {
  display: block;
  margin-left: auto;
  margin-right: auto;
  margin-top: 10%;
  width: 64px;
  height: 64px;
}
.lds-dual-ring:after {
  content: " ";
  display: block;
  width: 46px;
  height: 46px;
  margin: 1px;
  border-radius: 50%;
  border: 5px solid #cef;
  border-color: #cef transparent #cef transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}
@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }
  100% {
    transform: rotate(360deg);
  }
}
</style>

