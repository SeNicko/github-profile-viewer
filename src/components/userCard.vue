<template>
  <article class="profile">
    <img class="profile__image" :src="user.avatar_url" alt="Avatar of github account" />
    <header class="header">
      <span class="header__title">{{ user.login }}</span>
      <span class="header__subtitle">{{ user.name }}</span>
    </header>
    <main class="content mt">
      <p v-if="user.bio !== null">{{ user.bio }}</p>
      <a class="button mt" :href="user.html_url" target="_blank">
        Check on Github
      </a>
      <ul class="breadcrumb mt">
        <li class="breadcrumb__item">{{ formatNumber(user.followers) }} followers</li>
        <span class="breadcrumb__item--separator">&middot;</span>
        <li class="breadcrumb__item">{{ formatNumber(user.following) }} following</li>
        <span class="breadcrumb__item--separator">&middot;</span>
        <li class="breadcrumb__item">{{ formatNumber(user.public_repos) }} repos</li>
      </ul>
      <ul class="info mt">
        <li class="info__item" v-if="user.company">
          <img class="icon" src="@/assets/icons/company.svg" alt="Building icon" />
          <span>{{ user.company }}</span>
        </li>
        <li class="info__item" v-if="user.location">
          <img class="icon" src="@/assets/icons/location.svg" alt="Location icon" />
          <span>{{ user.location }}</span>
        </li>
        <li class="info__item" v-if="user.blog">
          <img class="icon" src="@/assets/icons/blog.svg" alt="Blog page icon" />
          <a :href="user.blog" target="_blank">{{ user.blog }}</a>
        </li>
        <li class="info__item" v-if="user.email">
          <img class="icon" src="@/assets/icons/mail.svg" alt="Mail icon" />
          <a :href="`mailto: ${user.email}`">{{ user.email }}</a>
        </li>
        <li class="info_item" v-if="user.twitter_username">
          <img class="icon" src="@/assets/icons/twitter.svg" alt="Twitter icon" />
          <a :href="`https://twitter.com/${user.twitter_username}`">@{{ user.twitter_username }}</a>
        </li>
      </ul>
    </main>
  </article>
</template>

<script>
import { formatNumber } from '@/util/utils';

export default {
  name: 'userCard',
  props: ['user'],
  data() {
    return {
      formatNumber,
    };
  },
};
</script>

<style lang="scss"></style>
