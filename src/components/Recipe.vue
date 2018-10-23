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

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
figure {
  margin: 4%;
}
</style>
