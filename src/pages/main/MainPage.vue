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
              @input="value !== '' ? getData(value) : ''"
              type="text"
              id="searchInput"
              name="search"
              class="header__form-input"
              placeholder="Enter GItHub login..."
              required
          >
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
  <main
      class="main"
      :class="{'height' : cardData.length < 3, 'heightfull' : cardData.length >= 3}"
  >
    <section class="hero">
      <div class="hero-wrap container">
        <div class="hero-space"></div>
        <ul
            v-if="cardData.length > 0"
            class="card-list"
        >
          <RepoCard
              v-for="(card, idx) in cardData"
              :key="idx"
          >
            <template #userAvatar>
              <a :href="card.html_url"
                 target="_blank"
                 class="card__img-link"
              >
                <img
                    :src="card.avatar_url"
                    alt="User avatar"
                    class="card__img"
                    width="1"
                    height="1"
                    loading="lazy"
                >
              </a>
            </template>
            <template #userInfo>
              <a :href="card.html_url" target="_blank" class="card__link">
                {{ card.name ?? 'Name is missing' }}
                &nbsp;<span> • </span>&nbsp;
                {{ card.login ?? '' }}
              </a>
            </template>
            <template #userBio>
              {{ card.bio }}
            </template>
            <template #followers>
              {{ card.followers }}
            </template>
            <template #following>
              {{ card.following }}
            </template>
            <template #repositories>
              {{ card.public_repos }}
            </template>
            <template #userRepo>
              <a
                  :href="card.html_url + '?tab=repositories'"
                  target="_blank"
                  class="btn card__info-btn"
              >
                Go to repository
              </a>
            </template>
            <template #userCreated>
              {{ new Date(card.created_at).toLocaleDateString() }}
            </template>
          </RepoCard>
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
      cardData: [],
    }
  },
  methods: {
    async getData(login) {
      return await fetch(`https://api.github.com/users/${login}`)
          .then(res => res.json())
          .then(res => {
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
