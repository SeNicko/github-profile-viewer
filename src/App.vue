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

<style>
@import url('https://fonts.googleapis.com/css2?family=Open+Sans:wght@400;600;700&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'Open Sans', sans-serif;
}

.button {
  cursor: pointer;
  border: 1px solid rgb(209, 209, 209);
  border-radius: 5px;
  outline: none;
  background: white;
  padding: 10px 15px;
  display: flex;
  align-items: center;
  width: fit-content;
  transition: 0.2s all ease-in-out;
}

.button:hover {
  background: rgb(250, 250, 250);
}

a {
  text-decoration: none;
  color: black;
  cursor: pointer;
  transition: 0.2s all ease-in-out;
}

a:hover {
  text-decoration: underline;
  color: rgb(0, 162, 255);
}

::-webkit-scrollbar {
  width: 25px; /* width of the entire scrollbar */
}
::-webkit-scrollbar-track {
  background: transparent; /* color of the tracking area */
}
::-webkit-scrollbar-thumb {
  background-color: rgb(209, 209, 209); /* color of the scroll thumb */
  border-left: 20px solid white;
}
</style>
