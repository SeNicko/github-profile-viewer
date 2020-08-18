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
  data() {
    return {
      search: '',
    };
  },
  methods: {
    updateSearchFilter() {
      const input = document.querySelector('input[name="username"]');
      this.search = input.value;
    },
  },
};
</script>
