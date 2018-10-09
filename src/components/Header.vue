<template>
    <section class="hero is-info">
    <div class="hero-head">
      <nav class="navbar">
        <div class="container">
          <div class="navbar-brand">
            <a class="navbar-item">
              <img src="https://bulma.io/images/bulma-type-white.png" alt="Logo">
            </a>
          </div>
          <div id="navbarMenuHeroB" class="navbar-menu">
            <div class="navbar-end">
              <span class="navbar-item">
                <a class="button is-info is-inverted" href="http://github.com/ngomez22/recipes-front">
                  <span class="icon">
                    <i class="fab fa-github"></i>
                  </span>
                  <span>View source</span>
                </a>
              </span>
            </div>
          </div>
        </div>
      </nav>
    </div>

    <div class="hero-body">
      <div class="container has-text-centered">
        <p class="title">
          Recipes
        </p>
        <p class="subtitle">
          by Nicolás Gómez
        </p>
      </div>
    </div>

    <div class="hero-foot">
      <nav class="tabs is-boxed is-fullwidth">
        <div class="container">
          <ul>
            <li class="is-active">
              <a>View Recipes</a>
            </li>
            <li>
              <a>Create Recipe</a>
            </li>
          </ul>
        </div>
      </nav>
    </div>
  </section>
</template>
