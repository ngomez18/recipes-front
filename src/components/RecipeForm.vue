<template>
  <div class="recipe-form">
    <p class="title">{{ editMode ? "Edit Recipe" : "New Recipe" }}</p>
      <div class="field">
        <label class="label">Name</label>
        <div class="control">
          <input class="input" type="text" placeholder="Scrambled eggs">
        </div>
      </div>

      <div class="field">
        <label class="label">Image</label>
        <div class="control">
          <input class="input" type="text" placeholder="https://i.imgur.com/HFEFssS.jpg">
        </div>
      </div>

      <div class="field">
        <label class="label">Description</label>
        <div class="control">
          <textarea class="textarea"
          placeholder="Delicious creamy scrambled eggs with bacon perfect for breakfast">
          </textarea>
        </div>
      </div>

      <div class="columns">
        <div class="field column">
          <label class="label">Required Time (in minutes)</label>
          <div class="control">
            <input class="input" type="number" placeholder="45">
          </div>
        </div>
        <div class="field column">
          <label class="label">Servings</label>
          <div class="control">
            <input class="input" type="number" placeholder="2">
          </div>
        </div>
        <div class="field column">
          <label class="label">Difficulty</label>
          <div class="control">
            <div class="select">
              <select>
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
        <textarea class="textarea"
        placeholder="Break 2 eggs into a bowl.
        Scramble.
        Sprinkle salt and pepper to taste.Pour on stove.
        Wait">
        </textarea>
      </div>
    </div>

    <div class="field is-grouped">
      <div class="control">
        <button class="button is-primary">Save</button>
      </div>
      <div class="control">
        <button class="button">Cancel</button>
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
        console.log(this.ingredients);
        this.ingredients.splice(index, 1);
        console.log(this.ingredient);
      }
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
