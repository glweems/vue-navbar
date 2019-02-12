<template>
  <div id="app">
    <small>default, Dark</small>
    <Navbar :brand="navbar.brand" :links="navbar.links" theme="dark" />
    <small>default, space-between</small>
    <Navbar :brand="navbar.brand" :links="navbar.links" type="space-between" />
    <small>light, space-evenly</small>
    <Navbar
      :brand="navbar.brand"
      :links="navbar.links"
      type="space-evenly"
      theme="light"
    />
    <small>light, dropdown</small>
    <Navbar
      :brand="navbar.brand"
      :links="navbar.links"
      mobile-dropdown
      type="space-between"
    />
    <div class="test">THIS IS A TEST</div>
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
        brand: "Brand",
        links: [
          { path: "#Home", name: "Home" },
          { path: "#About", name: "About" },
          { path: "#Contact", name: "Contact" },
          { path: "#Products", name: "Products" },
          { path: "#Location", name: "Location" }
        ]
      }
    };
  }
};
</script>

<style lang="scss">
body {
  font-size: 1.25rem;
}
$mobile-width: 640px;

@mixin mobile {
  @media (max-width: #{$mobile-width}) {
    @content;
  }
}

.test {
  width: 100%;
  background: salmon;
  @include mobile {
    width: 80%;
    margin: 0 auto;
  }
}

body {
  margin: 0;
  padding: 0;
  width: 100%;
}
</style>
