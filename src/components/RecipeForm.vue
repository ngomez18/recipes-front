<template>
  <div class="recipe-form">
    <p class="title">New Recipe</p>
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
                <option>1</option>
                <option>2</option>
                <option>3</option>
                <option>4</option>
                <option>5</option>
              </select>
            </div>
          </div> 
        </div>
      </div>

    <div class="ingredients">
      <label class="label">Ingredients</label>
      <div class="box content">
        <div class="field has-addons">
          <p class="control is-expanded">
            <input class="input" type="text" placeholder="Name">
          </p>
          <p class="control">
            <span class="select">
              <select>
                <option>Dairy</option>
                <option>Vegetable</option>
                <option>Meat</option>
                <option>Seasoning</option>
              </select>
            </span>
          </p>
          <a class="delete button is-danger is-medium">
            <span class="icon is-small">
              <i class="fas fa-times"></i>
            </span>
          </a>
        </div>
        <div class="container has-text-centered">
          <a class="button is-primary is-medium">
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
        <button class="button is-link">Submit</button>
      </div>
      <div class="control">
        <button class="button is-text">Cancel</button>
      </div>
    </div>
  </div>
</template>

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
