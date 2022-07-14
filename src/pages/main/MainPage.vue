<template>
  <header class="header">
    <div class="header-wrap container">
      <h1 class="header__title section-title">Search GitHub Repositories</h1>
      <div class="header__cta">
        <form
            action="#"
            class="header__form"
        >
          <!--@change="login !== '' ? getData(login) : ''"-->
          <input
              v-model="login"
              @input="login !== '' ? getData(login) : ''"
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
            <template
                #userAvatar
                v-if="card.avatar_url"
            >
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
            <template
                #userInfo
                v-if="card.login"
            >
              <a :href="card.html_url" target="_blank" class="card__link">
                {{ card.name ?? 'Name is missing' }}
                &nbsp;<span> • </span>&nbsp;
                {{ card.login }}
              </a>
            </template>
            <template
                #userBio
                v-if="card.bio"
            >
              {{ card.bio }}
            </template>
            <template
                #followers
                v-if="card.followers"
            >
              {{ card.followers }}
            </template>
            <template
                #following
                v-if="card.following"
            >
              {{ card.following }}
            </template>
            <template
                #repositories
                v-if="card.public_repos"
            >
              {{ card.public_repos }}
            </template>
            <template
                #userRepo
                v-if="card.html_url"
            >
              <a
                  :href="card.html_url + '?tab=repositories'"
                  target="_blank"
                  class="btn card__info-btn"
              >
                Go to repository
              </a>
            </template>
            <template
                #wishBtn
                v-if="card.login"
            >
              <button
                  @click="addToWishlist(card.login)"
                  type="button"
                  class="card__btn"
                  :class="{'active' : wishlist.includes(card.login)}"
              >
                <svg xmlns="http://www.w3.org/2000/svg"
                     width="32.000000pt" height="32.000000pt" viewBox="0 0 20.000000 10.000000">
                  <g transform="translate(0.000000,16.000000) scale(0.03,-0.03)"
                     fill="#fff" stroke="none">
                    <path d="M292 588 c-11 -24 -29 -71 -43 -105 l-23 -62 -108 -7 c-60 -3 -111 -11 -115 -17 -6 -10 33 -50 117 -119 l45 -37 -26 -105 c-20 -78 -23 -108 -15 -115 8 -7 40 8 99 45 48 30 93 54 100 54 6 0 50 -25 97 -55 57 -36 88 -51 96 -44 8 7 5 37 -14 114 l-26 105 44 37 c90 76 123 110 117 120 -4 6 -55 14 -115 18 l-107 7 -40 101 c-22 55 -46 102 -53 105 -7 2 -20 -15 -30 -40z"/>
                  </g>
                </svg>
              </button>
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
      login: '',
      cardData: [],
      recentList: [],
      wishlist: [],
    }
  },
  methods: {
    async getData(login) {
      return await fetch(`https://api.github.com/users/${login}`)
          .then(res => res.json())
          .then(res => {
            this.cardData.unshift(res);
            this.recentList.push(res);
            localStorage.setItem('recentList', JSON.stringify(this.recentList))
          })
    },
    addToWishlist(login) {
      if (!this.wishlist.includes(login)) {
        this.wishlist.push(login);
      } else {
        this.wishlist.splice(this.wishlist.indexOf(login), 1);
      }
      localStorage.setItem('wishlist', JSON.stringify(this.wishlist))
    },
  },
  mounted() {
    if (!localStorage.wishlist) {
      localStorage.wishlist = JSON.stringify([])
    } else if (localStorage.wishlist) {
      this.wishlist = JSON.parse(localStorage.wishlist);
    }
    if (!localStorage.recentList) {
      localStorage.recentList = JSON.stringify([])
    } else if (localStorage.recentList) {
      this.recentList = JSON.parse(localStorage.recentList);
    }
  },
}
</script>

<style lang="scss">
@import "../../assets/styles/pages/home-page/home-page";
</style>
