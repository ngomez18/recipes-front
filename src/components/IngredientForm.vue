<template>
  <div class="field has-addons">
    <p class="control is-expanded">
      <input v-model="ingredient.name" class="input" type="text" placeholder="Name">
    </p>
    <p class="control">
      <span class="select">
        <select v-model="ingredient.type">
          <option>Dairy</option>
          <option>Vegetable</option>
          <option>Meat</option>
          <option>Seasoning</option>
        </select>
      </span>
    </p>
    <a class="delete button is-danger is-medium"
       v-on:click="$emit('delete')">
      <span class="icon is-small">
        <i class="fas fa-times"></i>
      </span>
    </a>
  </div>
</template>

<script>
export default {
  name: 'ingredientForm',
  props: ['ingredient'],
};
</script>

