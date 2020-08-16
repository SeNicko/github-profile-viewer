<template>
  <nav class="navbar">
    <form @submit.prevent="submitForm">
      <input
        class="search-input space"
        name="username"
        type="text"
        placeholder="Find a github user!"
        autocomplete="off"
      />
      <button type="submit" class="search-button space">
        Search
      </button>
    </form>
  </nav>
</template>

<script>
export default {
  props: ['submitForm'],
};
</script>

<style scoped>
.navbar {
  width: 100vw;
  height: 60px;
  display: flex;
  align-items: center;
  justify-content: center;
  border-bottom: 0.5px solid rgb(226, 226, 226);
}

.search-input {
  width: 500px;
  padding: 10px;
  border: 1px solid rgb(150, 150, 150);
  border-radius: 5px;
}

.search-button {
  border: none;
  background: rgb(25, 114, 230);
  color: white;
  padding: 10px;
  border-radius: 5px;
  outline: none;
  cursor: pointer;
}

.search-button:hover {
  border: none;
  background: rgb(19, 96, 197);
  color: white;
  padding: 10px;
  border-radius: 5px;
  outline: none;
  cursor: pointer;
  transition: 0.2s all ease-in-out;
}

.space {
  margin: 0 5px;
}
</style>
