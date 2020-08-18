<template>
  <nav class="navbar">
    <form @submit.prevent="submitForm">
      <input
        class="navbar__input space"
        name="username"
        type="text"
        placeholder="Find a github user!"
        autocomplete="off"
      />
      <button type="submit" class="navbar__button space">
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
