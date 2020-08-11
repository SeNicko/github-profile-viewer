<template>
  <div class="home">
    <div class="container">
      <div class="card">
        <section class="content">
          <img :src="user.avatar_url" class="avatar" alt="Avatar of github account" />
          <span class="section-item login">{{ user.login }}</span>
          <span class="section-item small">{{ user.name }}</span>
        </section>
        <br />
        <section>
          <p>{{ user.bio }}</p>
        </section>
        <br />
        <section class="breadcrumb">
          <a class="link" href="#"> {{ user.followers }} followers</a>
          <span class="wall">/</span>
          <a class="link" href="#"> {{ user.following }} following</a>
          <span class="wall">/</span>
          <a class="link" href="#"> {{ user.public_repos }} public repositories</a>
        </section>
        <br />
        <section class="info">
          <span class="section-item" v-if="user.location">📌 {{ user.location }}</span>
          <span class="section-item" v-if="user.blog">
            <a :href="user.blog" class="link"> 💻 {{ user.blog }} </a>
          </span>
          <span class="section-item" v-if="user.email">📫 {{ user.email }}</span>
          <span class="section-item" v-if="user.twitter_username"
            ><img class="icon" src="@/assets/Twitter_Logo_Blue.svg" alt="" /> @{{
              user.twitter_username
            }}</span
          >
        </section>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['search'],
  data: () => ({
    user: {},
  }),
  methods: {
    async get(url) {
      const response = await fetch(url);
      const json = await response.json();

      return json;
    },
    async findUser(username) {
      const API_URL = 'https://api.github.com/users';
      this.user = await this.get(`${API_URL}/${username}`);
    },
  },
  watch: {
    search(val) {
      this.findUser(val);
    },
  },
};
</script>

<style>
.card {
  width: 500px;
}

.avatar {
  width: 100%;
  height: auto;
  border-radius: 10px;
}

.icon {
  width: 30px;
  height: auto;
}

.login {
  font-size: 28px;
}

.section-item {
  display: block;
}

.small {
  font-size: 16px;
  color: gray;
}

.link {
  text-decoration: none;
  color: black;
  transition: 0.1s all ease-in-out;
}

.link:hover {
  text-decoration: none;
  color: rgb(0, 140, 255);
}

.breadcrumb .wall {
  margin: 0 8px;
}

.container {
  display: flex;
  justify-content: center;
  flex-direction: column;
  align-items: center;
}
</style>
