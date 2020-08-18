<template>
  <article class="repository mt">
    <header class="header">
      <span>{{ repository.name }}</span>
      <a :href="repository.html_url" class="header__subtitle --align-vertical" target="_blank">
        <img src="@/assets/icons/link.svg" alt="Link image" class="icon" />
        <span>{{ repository.full_name }}</span>
      </a>
    </header>
    <main class="mt" v-if="repository.description !== null">
      <p>{{ repository.description }}</p>
      <ul class="breadcrumb mt">
        <li class="breadcrumb__item" title="watchers">
          <img class="icon" src="@/assets/icons/eye.svg" alt="Eye icon" />
          <span>{{ formatNumber(repository.watchers_count) }}</span>
        </li>
        <span class="breadcrumb__item--separator">&middot;</span>
        <li class="breadcrumb__item" title="stars">
          <img class="icon" src="@/assets/icons/star.svg" alt="Star icon" />
          <span>{{ formatNumber(repository.stargazers_count) }}</span>
        </li>
        <span class="breadcrumb__item--separator">&middot;</span>
        <li class="breadcrumb__item" title="forks">
          <img class="icon" src="@/assets/icons/code-fork.svg" alt="Code fork icon" />
          <span>{{ formatNumber(repository.forks_count) }}</span>
        </li>
      </ul>
      <section class="language mt" v-if="repository.language">
        <span
          class="language__label"
          :style="{
            background: colors[`${repository.language}`] || 'white',
          }"
        ></span>
        <span>{{ repository.language }}</span>
      </section>
    </main>
  </article>
</template>

<script>
import { colors, formatNumber } from '@/util/utils';

export default {
  props: ['repository'],
  data() {
    return {
      formatNumber,
      colors,
    };
  },
};
</script>
