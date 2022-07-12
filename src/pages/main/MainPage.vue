<template>
  <header class="header">
    <div class="header-wrap container">
      <h1 class="header__title section-title">Search GitHub Repositories</h1>
      <div class="header__cta">
        <form
            action="#"
            class="header__form"
        >
          <input
              v-model="value"
              type="text"
              id="searchInput"
              name="search"
              class="header__form-input"
              placeholder="Enter GItHub login..."
              required
          >
          <br>
          <button
              id="searchBtn"
              type="submit"
              class="btn header__form-btn"
          >
            Search
          </button>
        </form>
        <router-link
            to="/wishlist"
            class="btn header__btn"
        >
          Go to Wishlist &#10143;
        </router-link>
      </div>
    </div>
  </header>
  <main class="main">
    <section class="hero">
      <ul class="card-list">

      </ul>
    </section>
  </main>
</template>

<script>
export default {
  name: "MainPage",
  data() {
    return {
      value: '',
    }
  }
}
</script>

<style lang="scss">
@import "../../assets/styles/pages/home-page/home-page";
</style>
