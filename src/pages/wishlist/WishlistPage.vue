<template>
  <header class="header">
    <div class="header-wrap container">
      <h1 class="header__title section-title">Wishlist</h1>
    </div>
  </header>
  <main class="main">
<!--      :class="{'height' : cardData.length < 3, 'heightfull' : cardData.length >= 3}"-->
    <section class="hero">
      <ul class="card-list">

      </ul>
    </section>
  </main>
</template>

<script>
export default {
  name: "wishlistPage"
}
</script>

<style lang="scss">
@import "../../assets/styles/pages/wishlist-page/wishlist-page";
</style>
