<template>
  <li class="card">
    <div class="card__top">
      <slot name="userAvatar">
        <div class="card__img-link">
          <img
              src="https://specialplantzundert.nl/wp-content/uploads/2020/06/not-found-image-15383864787lu-300x226.jpg"
              alt="User avatar"
              class="card__img"
              style="height: 195px"
              width="1"
              height="1"
              loading="lazy"
          >
        </div>
      </slot>
      <div class="card__info">
        <slot name="userInfo">
          <p class="card__link card__link--not-underline" >
            User doesn't exist
          </p>
        </slot>
        <p class="card__description">
          <slot name="userBio">User bio is missing</slot>
        </p>
        <ul class="card__info-list">
          <li class="card__info-item">
            Followers: <slot name="followers">-</slot>
          </li>
          <li class="card__info-item">
            Following: <slot name="following">-</slot>
          </li>
          <li class="card__info-item">
            Public repositories: <slot name="repositories">-</slot>
          </li>
        </ul>
        <slot name="userRepo"></slot>
        <slot name="wishBtn"></slot>
      </div>
    </div>
    <div class="card__footer">
      <p class="card__created">
        Created: <slot name="userCreated">Invalid Date</slot>
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
