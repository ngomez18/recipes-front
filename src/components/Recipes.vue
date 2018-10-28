<template>
  <div id="recipes">
    <div class="title has-text-centered no-recipes"
        v-if="recipes.length == 0">
      <p>No recipes available</p>
    </div>
    <div class="columns is-multiline">
      <Recipe v-for="recipe in recipes"
              v-bind:recipe="recipe"
              v-bind:key="recipe.ID"
              v-on:delete="deleteRecipe(recipe.ID)" />
    </div>
  </div>
</template>

<script>
import axios from 'axios';
import swal from 'sweetalert';
import Recipe from './Recipe.vue';

export default {
  name: 'recipes',
  components: {
    Recipe,
  },

  data() {
    return {
      recipes: [],
    };
  },

  mounted() {
    this.fetchRecipes();
  },

  methods: {
    fetchRecipes() {
      axios.get('https://recipes-api-go.herokuapp.com/api/recipes')
        .then(response => (this.recipes = response.data))
        .catch(error => console.log(error));
    },
    deleteRecipe(id) {
      const vm = this; // View Model
      swal('Are you sure you want to delete this recipe?', {
        dangerMode: true,
        buttons: true,
      }).then((isConfirm) => {
        if (isConfirm) {
          axios.delete(`https://recipes-api-go.herokuapp.com/api/recipe/${id}`)
            .then((response) => {
              console.log(response);
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
        }
      });
    },
  },
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.columns {
  padding: 4%;
}

.no-recipes {
  margin-top: 7%;
  display: flex;
  justify-content: center;
}
</style>
