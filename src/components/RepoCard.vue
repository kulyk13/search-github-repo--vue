<template>
  <li class="card">
    <div class="card__top">
      <slot name="userAvatar">
        <a href="#" class="card__img-link">
          <img
              src="https://www.fillmurray.com/640/360"
              alt="User avatar"
              class="card__img"
              width="1"
              height="1"
              loading="lazy"
          >
        </a>
      </slot>
      <div class="card__info">
        <slot name="userInfo">
          <a
              href="#"
              target="_blank"
              class="card__link"
          >
            User name
            &nbsp;<span> • </span>&nbsp;
            User login
          </a>
        </slot>
        <p class="card__description">
          <slot name="userBio">User bio is missing</slot>
        </p>
        <ul class="card__info-list">
          <li class="card__info-item">
            Followers: <slot name="followers">0</slot>
          </li>
          <li class="card__info-item">
            Following: <slot name="following">0</slot>
          </li>
          <li class="card__info-item">
            Public repositories: <slot name="repositories">0</slot>
          </li>
        </ul>
        <slot name="userRepo">
          <a
              href="#"
              target="_blank"
              class="btn card__info-btn"
          >
            Go to repository
          </a>
        </slot>
        <button
            type="button"
            class="card__btn"
        >
          <svg xmlns="http://www.w3.org/2000/svg"
               width="32.000000pt" height="32.000000pt" viewBox="0 0 20.000000 10.000000">
            <g transform="translate(0.000000,16.000000) scale(0.03,-0.03)"
               fill="#fff" stroke="none">
              <path d="M292 588 c-11 -24 -29 -71 -43 -105 l-23 -62 -108 -7 c-60 -3 -111
                    -11 -115 -17 -6 -10 33 -50 117 -119 l45 -37 -26 -105 c-20 -78 -23 -108 -15
                    -115 8 -7 40 8 99 45 48 30 93 54 100 54 6 0 50 -25 97 -55 57 -36 88 -51 96
                    -44 8 7 5 37 -14 114 l-26 105 44 37 c90 76 123 110 117 120 -4 6 -55 14 -115
                    18 l-107 7 -40 101 c-22 55 -46 102 -53 105 -7 2 -20 -15 -30 -40z"/>
            </g>
          </svg>
        </button>
      </div>
    </div>
    <div class="card__footer">
      <p class="card__created">
        Created: <slot name="userCreated">01.01.2000</slot>
      </p>
    </div>
  </li>
</template>

<script>
export default {
  name: "RepoCard",
}
</script>

<style lang="scss">
@import "../assets/styles/components/repo-card";
</style>
