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
              @input="getData(value)"
              type="text"
              id="searchInput"
              name="search"
              class="header__form-input"
              placeholder="Enter GItHub login..."
              required
          >
          <br>
          <button
              @submit="getData(value)"
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
      <div class="hero-wrap container">
        <div class="hero-space"></div>
        <ul class="card-list">
          <RepoCard></RepoCard>
        </ul>
      </div>
    </section>
  </main>
</template>

<script>
import RepoCard from "@/components/RepoCard";
export default {
  name: "MainPage",
  components: {
    RepoCard
  },
  data() {
    return {
      value: '',
      cardData: [

      ]
    }
  },
  methods: {
    async getData(login) {
      return await fetch(`https://api.github.com/users/${login}`)
          .then(res => res.json())
          .then(res => {
            // this.cardData.unshift(JSON.stringify(res));
            this.cardData.unshift(res);
            console.log(this.cardData)
          })
    }
  }
}
</script>

<style lang="scss">
@import "../../assets/styles/pages/home-page/home-page";
</style>
