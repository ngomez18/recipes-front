<template>
  <div id="recipes" class="tile is-ancestor">
    <div class="tile is-parent columns">
      <Recipe />
      <Recipe />
      <Recipe />
    </div>
  </div>
</template>

<script>
import Recipe from './Recipe.vue';

export default {
  name: 'recipes',
  components: {
    Recipe,
  },
};
</script>


<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped lang="scss">
.columns {
  padding: 4%;
}
</style>
