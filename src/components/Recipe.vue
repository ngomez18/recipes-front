<template>
  <article class="tile is-child column is-4 box">
    <p class="title">Recipe name</p>
    <p>Lorem ipsum dolor sit amet, consectetur adipiscing elit. Vestibulum placerat ligula ipsum,
      scelerisque tincidunt nunc posuere a.Integer nec lorem pharetra, ultrices augue ut,
      tincidunt.</p>
    <figure class="image is-3by2">
      <!-- Placeholder image -->
      <img src="https://images.unsplash.com/photo-1503764654157-72d979d9af2f">
    </figure>
    <div class="box level">
      <span class="icon">
        <i class="fas fa-clock"></i>
      </span>
      <p>45 min</p>
      <span class="icon">
        <i class="fas fa-users"></i>
      </span>
      <p>Serves 4</p>
      <span class="icon">
        <i class="fas fa-tachometer-alt"></i>
      </span>
      <p> {{ getDifficultyText(1) }} </p>
    </div>
    <table class="table is-fullwidth">
      <thead>
        <tr>
          <th>Ingredients</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>Hola</td>
        </tr>
      </tbody>
    </table>
    <table class="table">
      <thead>
        <tr>
          <th>Instructions</th>
        </tr>
      </thead>
      <tbody>
        <tr>
          <td>fjkasdfjasdlfkjasdlfkjasdlfkjañsldfjañsldfkjañsldfkjañsldfkj</td>
        </tr>
      </tbody>
    </table>
    <div class="field is-grouped">
      <p class="control has-centered-text">
        <a class="button is-link">
          <span class="fa fa-edit"></span>
          Edit
        </a>
      </p>
      <p class="control">
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
</style>
