<template>
  <article class="column is-two-fifths box">
    <p class="title">{{ recipe.name }}</p>
    <p>{{ recipe.description }}</p>
    <figure class="image is-3by2">
      <img v-bind:src="recipe.image">
    </figure>
    <div class="box level">
      <span class="icon">
        <i class="fas fa-clock"></i>
      </span>
      <p>{{ recipe.requiredTime }} min</p>
      <span class="icon">
        <i class="fas fa-users"></i>
      </span>
      <p>Serves {{ recipe.servings }}</p>
      <span class="icon">
        <i class="fas fa-tachometer-alt"></i>
      </span>
      <p> {{ getDifficultyText(recipe.difficulty) }} </p>
    </div>
    <table class="table is-fullwidth">
      <thead>
        <tr>
          <th>Ingredients</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="ingredient in recipe.ingredients"
            v-bind:key="ingredient.name">
          <td>{{ ingredient.name + " (" + ingredient.type + ")"}}</td>
        </tr>
      </tbody>
    </table>
    <table class="table is-fullwidth">
      <thead>
        <tr>
          <th>Instructions</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>{{ recipe.steps }}</td>
        </tr>
      </tbody>
    </table>
    <div class="field is-grouped">
      <p class="control has-centered-text"
        v-on:click="$emit('edit')">
        <a class="button is-link">
          <span class="fa fa-edit"></span>
          Edit
        </a>
      </p>
      <p class="control"
        v-on:click="$emit('delete')">
        <a class="button is-danger">
          <span class="fa fa-trash"></span>
          Delete
        </a>
      </p>
    </div>
  </article>
</template>

<script>
export default {
  name: 'recipe',
  props: ['recipe'],

  methods: {
    getDifficultyText(diff) {
      switch (diff) {
        case 1: return 'Very easy';
        case 2: return 'Easy';
        case 3: return 'Intermediate';
        case 4: return 'Hard';
        case 5: return 'Very Hard';
        default: return 'Unknown difficulty';
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
figure {
  margin: 4%;
}
article {
  margin: 2.5%;
}
</style>
