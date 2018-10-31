<template>
  <div class="recipe-form">
    <p class="title">{{ editMode ? "Edit Recipe" : "New Recipe" }}</p>
      <div class="field">
        <label class="label">Name</label>
        <div class="control">
          <input v-model="recipe.name" class="input" type="text"
                placeholder="Ham and cheese sandwich">
        </div>
      </div>

      <div class="field">
        <label class="label">Image</label>
        <div class="control">
          <input v-model="recipe.image" class="input" type="text"
                placeholder="https://i.imgur.com/HFEFssS.jpg">
        </div>
      </div>

      <div class="field">
        <label class="label">Description</label>
        <div class="control">
          <textarea v-model="recipe.description" class="textarea"
          placeholder="Yummy sandwich perfect for any occasion">
          </textarea>
        </div>
      </div>

      <div class="columns">
        <div class="field column">
          <label class="label">Required Time (in minutes)</label>
          <div class="control">
            <input v-model="recipe.requiredTime" class="input" type="number" placeholder="15">
          </div>
        </div>
        <div class="field column">
          <label class="label">Servings</label>
          <div class="control">
            <input v-model="recipe.servings" class="input" type="number" placeholder="1">
          </div>
        </div>
        <div class="field column">
          <label class="label">Difficulty</label>
          <div class="control">
            <div class="select">
              <select v-model="recipe.difficulty">
                <option v-for="i in 5"
                        v-bind:key="i">{{ i }}</option>
              </select>
            </div>
          </div>
        </div>
      </div>

    <div class="ingredients">
      <label class="label">Ingredients</label>
      <div class="box content">
        <IngredientForm v-for="(ingredient, index) in ingredients"
                        v-bind:key="index"
                        v-bind:ingredient="ingredient"
                        v-bind:types="ingredientTypes"
                        v-on:delete="deleteIngredient(index)"/>
        <div class="container has-text-centered">
          <a class="button is-primary"
             v-on:click="addIngredient">
            <span class="icon is-medium">
              <i class="fas fa-plus"></i>
            </span>
          </a>
        </div>
      </div>
    </div>

    <br>
    <div class="field">
      <label class="label">Instructions</label>
      <div class="control">
        <textarea v-model="recipe.steps" class="textarea"
        placeholder="Place a slice of ham and a slice of cheese on top of a loaf of bread.
        Place another loaf of bread on top of the ham and cheese and enjoy!">
        </textarea>
      </div>
    </div>

    <div class="field is-grouped">
      <div class="control">
        <button v-on:click="saveRecipe" class="button is-primary">Save</button>
      </div>
      <div class="control">
        <button v-on:click="$emit('cancel')" class="button">Cancel</button>
      </div>
    </div>
  </div>
</template>

<script>
import swal from 'sweetalert';
import IngredientForm from './IngredientForm.vue';

export default {
  name: 'recipeForm',
  props: ['editMode', 'recipe'],

  components: {
    IngredientForm,
  },

  data() {
    return {
      ingredients: [
        {
          name: '',
          type: '',
        },
      ],
      ingredientTypes: [
        'Vegetable',
        'Spice/Herb',
        'Cereal',
        'Meat',
        'Dairy',
        'Fruit',
        'Seafood',
        'Sugar',
        'Nut',
        'Other',
      ],
    };
  },

  watch: {
    recipe(newVal) {
      this.ingredients = newVal.ingredients;
    },
  },

  methods: {
    addIngredient() {
      this.ingredients.push({
        name: '',
        type: '',
      });
    },
    deleteIngredient(index) {
      if (this.ingredients.length <= 1) {
        swal('Surely your recipe requires at least one ingredient!');
      } else {
        this.ingredients.splice(index, 1);
      }
    },
    saveRecipe() {
      if (!this.recipe.name || !this.recipe.image || !this.recipe.description
        || !this.recipe.requiredTime || !this.recipe.servings || !this.recipe.difficulty
        || !this.checkIngredients() || !this.recipe.steps) {
        swal('All fields are mandatory! Please make sure to fill them all out');
      } else if (!this.isImageURL(this.recipe.image)) {
        swal('Please provide a valid image link for your recipe');
      } else {
        this.recipe.ingredients = this.ingredients;
        this.recipe.requiredTime = parseInt(this.recipe.requiredTime, 10);
        this.recipe.servings = parseInt(this.recipe.servings, 10);
        this.recipe.difficulty = parseInt(this.recipe.difficulty, 10);
        this.$emit('save', this.recipe);
      }
    },
    isImageURL(url) {
      return (url.match(/\.(jpeg|jpg|gif|png)$/) !== null);
    },
    checkIngredients() {
      return this.ingredients.every(ingredient => (ingredient.name && ingredient.type));
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
 .delete {
  padding: 1%;
  margin-left: 1%;
 }

 .recipe-form {
  margin: 5%;
 }
</style>
