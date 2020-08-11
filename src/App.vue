<template>
  <div id="app">
    <Navbar :submitForm="updateSearchFilter" />
    <router-view :search="search" />
  </div>
</template>

<script>
import Navbar from '@/components/Navbar.vue';

export default {
  components: {
    Navbar,
  },
  data: () => ({
    search: '',
  }),
  methods: {
    updateSearchFilter() {
      const input = document.querySelector('input[name="username"]');
      this.search = input.value;
    },
  },
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600;700&display=swap');

* {
  margin: 0;
  box-sizing: border-box;
  font-family: 'Open Sans', sans-serif;
}

button {
  cursor: pointer;
}
</style>
