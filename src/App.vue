<template>
  <div id="app">
    <Navbar :brand="navbar.brand" :links="navbar.links" />
  </div>
</template>

<script>
import Navbar from "./components/Navbar.vue";

export default {
  name: "App",
  components: {
    Navbar
  },
  data() {
    return {
      navbar: {
        brand: "Nav Brand",
        links: [
          { path: "/", name: "Home" },
          { path: "/", name: "About" },
          { path: "/", name: "Contact" },
          { path: "/", name: "Products" }
        ]
      }
    };
  }
};
</script>

<style lang="scss">
body {
  margin: 0;
  padding: 0;
  width: 100%;
}
</style>
