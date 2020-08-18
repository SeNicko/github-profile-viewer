<template>
  <div class="home" v-if="Object.keys(user).length > 0">
    <userCard :user="user"></userCard>
    <section class="repositories ml">
      <nav style="position: sticky; top: 0; display: flex;">
        <button class="button" @click="prevReposPage()" :disabled="currentReposPage <= 1">
          prev
        </button>
        <button
          class="button"
          @click="nextReposPage()"
          :disabled="currentReposPage >= numberOfReposPages"
        >
          next
        </button>
      </nav>

      <repositoryCard
        v-for="repository in repositories"
        :key="repository.id"
        :repository="repository"
      ></repositoryCard>
    </section>
  </div>
</template>

<script>
import userCard from '@/components/userCard.vue';
import repositoryCard from '@/components/repositoryCard.vue';

import { formatNumber } from '@/util/utils';

const API_URL = 'https://api.github.com/users';

export default {
  props: ['search'],
  name: 'Home',
  components: {
    userCard,
    repositoryCard,
  },
  data: () => ({
    user: {},
    repositories: [],
    currentReposPage: 1,
    numberOfReposPages: 1,
    reposPageSize: 30,
    formatNumber,
  }),
  methods: {
    fetchUserData(username) {
      fetch(`${API_URL}/${username}`)
        .then((response) => response.json())
        .then((user) => {
          this.user = user;
        })
        .catch((err) => console.error(err));
    },
    fetchRepositories(username) {
      fetch(
        `${API_URL}/${username}/repos?page=${this.currentReposPage}&per_page=${this.reposPageSize}`,
      )
        .then((response) => {
          const linkHeader = response.headers.get('link');
          if (linkHeader) {
            const lastPageLink = linkHeader.split(',')[1];
            const indexOfPageParam = lastPageLink.indexOf('page=') + 5;
            const endIndex = lastPageLink.indexOf('&');
            this.numberOfReposPages = lastPageLink.slice(indexOfPageParam, endIndex);
          }

          return response.json();
        })
        .then((repos) => {
          this.repositories = repos;
        })
        .catch((err) => console.error(err));
    },
    prevReposPage() {
      if (this.currentReposPage > 1) {
        this.currentReposPage -= 1;
        this.fetchRepositories(this.search);
      }
    },
    nextReposPage() {
      if (this.currentReposPage < this.numberOfReposPages) {
        this.currentReposPage += 1;
        this.fetchRepositories(this.search);
      }
    },
  },
  watch: {
    search(username) {
      this.fetchUserData(username);
      this.fetchRepositories(username);
    },
  },
};
</script>
