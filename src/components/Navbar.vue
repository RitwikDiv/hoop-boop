<template>
  <div class="container">
    <router-link to="/home">{{ name }}</router-link>
    <router-link to="/about"> About </router-link>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  data() {
    return {
      name: "Hoop Boop",
    };
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
</style>
