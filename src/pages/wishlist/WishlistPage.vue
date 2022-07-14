<template>
  <header class="wish-header header">
    <div class="wish-header__wrap header-wrap container">
      <h1 class="header__title section-title">Wishlist</h1>
      <router-link
          to="/"
          class="btn wish-header__btn"
      >

        &#129044; Back to Search
      </router-link>
    </div>
  </header>
  <main
      class="main"
      :class="{'height' : wishlist.length < 3, 'heightfull' : wishlist.length >= 3}"
      >
    <section class="hero">
      <div class="hero-wrap container">
        <ul class="card-list">
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
            <template #wishBtn>
              <button
                  @click="removeFromWishlist(card.login)"
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
  name: "wishlistPage",
  components: {
    RepoCard
  },
  data() {
    return {
      cardData: [],
      recentList: JSON.parse(localStorage.recentList),
      wishlist: JSON.parse(localStorage.wishlist),
    }
  },
  methods: {
    removeFromWishlist(login) {
      this.wishlist.splice(this.wishlist.indexOf(login), 1);
      localStorage.setItem('wishlist', JSON.stringify(this.wishlist))
    },
  },
  mounted() {
    console.log(this.recentList)
    console.log(this.wishlist)
    this.cardData = this.wishlist.reduce((acc, curr) => {
      return [...acc, this.recentList.find(repo => repo.login === curr)]
    }, [])
  }
}
</script>

<style lang="scss">
@import "../../assets/styles/pages/wishlist-page/wishlist-page";
</style>
