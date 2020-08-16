<template>
  <div class="home">
    <div class="container" v-if="Object.keys(user).length > 0">
      <section class="card">
        <section class="card-item">
          <img :src="user.avatar_url" class="avatar" alt="Avatar of github account" />
          <h1 class="large">{{ user.login }}</h1>
          <p class="small">{{ user.name }}</p>
        </section>
        <section class="card-item" v-if="user.bio !== null">
          <p>{{ user.bio }}</p>
        </section>
        <a class="button card-item" :href="user.html_url" target="_blank">
          <span>Check on Github</span>
        </a>
        <ul class="breadcrumb card-item">
          <li class="breadcrumb-item">{{ user.followers }} followers</li>
          <span class="breadcrumb-separator">&middot;</span>
          <li class="breadcrumb-item">{{ user.following }} following</li>
          <span class="breadcrumb-separator">&middot;</span>
          <li class="breadcrumb-item">{{ user.public_repos }} repos</li>
        </ul>
        <ul class="info card-item">
          <li>
            <div class="align-vertical" v-if="user.company">
              <img class="icon" src="@/assets/company.svg" alt="Building icon" />
              <span>{{ user.company }}</span>
            </div>
          </li>
          <li>
            <div class="align-vertical" v-if="user.location">
              <img class="icon" src="@/assets/location.svg" alt="Location icon" />
              <span>{{ user.location }}</span>
            </div>
          </li>
          <li>
            <div class="align-vertical" v-if="user.blog">
              <img class="icon" src="@/assets/blog.svg" alt="Blog page icon" />
              <a :href="user.blog" target="_blank">{{ user.blog }}</a>
            </div>
          </li>
          <li>
            <div class="align-vertical" v-if="user.email">
              <img class="icon" src="@/assets/mail.svg" alt="Mail icon" />
              <a :href="`mailto: ${user.email}`">{{ user.email }}</a>
            </div>
          </li>
          <li>
            <div class="align-vertical" v-if="user.twitter_username">
              <img class="icon" src="@/assets/twitter.svg" alt="Twitter icon" />
              <a :href="`https://twitter.com/${user.twitter_username}`"
                >@{{ user.twitter_username }}</a
              >
            </div>
          </li>
        </ul>
      </section>
      <section class="repositories">
        <div class="card repositories-item" v-for="repository in repositories" :key="repository.id">
          <section class="card-item">
            <p>
              {{ repository.name }}
            </p>
            <a :href="repository.html_url" class="small align-vertical" target="_blank">
              <img src="@/assets/link.svg" alt="Link image" class="icon" />
              {{ repository.full_name }}
            </a>
          </section>
          <section class="card-item" v-if="repository.description !== null">
            <p>
              {{ repository.description }}
            </p>
          </section>
          <ul class="breadcrumb card-item">
            <li class="breadcrumb-item" title="watchers">
              <span class="align-vertical">
                <img class="icon" src="@/assets/eye.svg" alt="Eye icon" />
                <span>{{ repository.watchers_count }}</span>
              </span>
            </li>
            <span class="breadcrumb-separator">&middot;</span>
            <li class="breadcrumb-item" title="stars">
              <span class="align-vertical">
                <img class="icon" src="@/assets/star.svg" alt="Star icon" />
                <span>{{ repository.stargazers_count }}</span>
              </span>
            </li>
            <span class="breadcrumb-separator">&middot;</span>
            <li class="breadcrumb-item" title="forks">
              <span class="align-vertical">
                <img class="icon" src="@/assets/code-fork.svg" alt="Code fork icon" />
                <span>{{ repository.forks_count }}</span>
              </span>
            </li>
          </ul>
          <div class="align-vertical" v-if="repository.language">
            <div
              class="language-label"
              :style="{ background: colors[`${repository.language}`] || 'white' }"
            ></div>
            <span>{{ repository.language }}</span>
          </div>
        </div>
      </section>
    </div>
  </div>
</template>

<script>
import colors from '@/util/colors.json';

const API_URL = 'https://api.github.com/users';

const get = async (url) => {
  const response = await fetch(url);
  const json = await response.json();

  return json;
};

export default {
  props: ['search'],
  name: 'Home',
  data: () => ({
    user: {},
    repositories: {},
    colors,
  }),
  methods: {
    async findUser(username) {
      this.user = await get(`${API_URL}/${username}`);
      this.repositories = await get(`${API_URL}/${username}/repos?page=1&per_page=30`);
    },
  },
  watch: {
    search(username) {
      this.findUser(username);
    },
  },
};
</script>

<style>
.info {
  list-style-type: none;
}

.info li {
  margin-bottom: 0.5rem;
}

.card {
  width: 500px;
}

.card .card-item:not(:last-child) {
  margin-bottom: 1.2rem;
}

.avatar {
  width: 100%;
  height: auto;
  border-radius: 10px;
  border: 0.2px solid lightgray;
}

.icon {
  width: 18px;
  height: auto;
  margin-right: 10px;
}

.large {
  font-size: 28px;
  font-weight: 500;
}

.align-vertical {
  display: flex;
  align-content: center;
}

.small {
  font-size: 16px;
  color: gray;
}

.link {
  text-decoration: none;
  color: black;
  transition: 0.2s all ease-in-out;
}

.link:hover {
  text-decoration: none;
  color: rgb(0, 140, 255);
}

.breadcrumb {
  display: flex;
  align-items: center;
}

.breadcrumb .breadcrumb-item {
  display: inline-block;
}

.breadcrumb .breadcrumb-separator {
  margin: 0 0.5rem;
}

.container {
  display: flex;
  justify-content: center;
}

.repositories {
  height: calc(100vh - 60px);
  width: 700px;
  box-sizing: content-box;
  overflow-y: scroll;
  margin-left: 15px;
}

.repositories-item {
  border: 0.2px solid lightgray;
  border-radius: 10px;
  padding: 15px;
  height: fit-content;
  width: 100%;
}

.repositories-item:nth-child(n + 2) {
  margin-top: 15px;
}

.language-label {
  width: 15px;
  height: 15px;
  border-radius: 15px;
  border: 1px solid black;
  margin-right: 15px;
}
</style>
