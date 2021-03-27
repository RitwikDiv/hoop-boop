<template>
  <div
    class="container d-flex flex-column flex-md-row align-items-center p-3 px-md-4 mb-3 bg-white box-shadow"
  >
    <h2 class="my-0 mr-md-auto font-weight-bold">{{ name }}</h2>
    <nav class="my-4 my-md-4">
      <router-link to="/home" class="p-2 nav-item text-muted mr-3">
        <strong>Memories</strong>
      </router-link>
      <router-link to="/notes" class="p-2 nav-item text-muted ml-3">
        <strong>Notes</strong>
      </router-link>
    </nav>
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
.nav-item {
  font-size: 1.1em;
}
</style>
