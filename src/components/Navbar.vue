<template>
  <div id="navbar" :class="navSettings">
    <!-- Navbar Brand -->
    <div class="nav-container navbar-brand">
      <a href="/">{{ brand }}</a>
    </div>
    <!-- Navlinks / Dropdown-Button -->
    <div class="nav-container">
      <!-- <button v-if="dropdown">dropdown</button> -->
      <!-- Nav-Links -->
      <nav class="nav-links">
        <a v-for="(link, index) in links" :key="index" :href="link.path">
          {{ link.name }}
        </a>
      </nav>
    </div>
  </div>
</template>

<script>
export default {
  name: "Navbar",
  props: {
    links: {
      type: Array,
      required: true,
      default() {
        return [
          { path: "#1", name: "Link 1" },
          { path: "#2", name: "link 2" },
          { path: "#3", name: "link 3" }
        ];
      },
      validator: function(items) {
        let hasName = true;
        let hasPath = true;
        items.forEach(item => {
          if (!item.path || typeof item.name !== "string") {
            hasPath = false;
          }
          if (!item.name) {
            hasName = false;
          }
        });
        return hasPath && hasName;
      }
    },
    brand: {
      type: String,
      default: "Brand",
      validator(brand) {
        return String(brand);
      }
    },
    theme: {
      type: String,
      default: "default",
      validator: function(value) {
        return ["default", "light", "dark"].indexOf(value) !== -1;
      }
    },
    type: {
      type: String,
      default: "start",
      validator: function(value) {
        return (
          [
            "start",
            "center",
            "space-between",
            "space-evenly",
            "scroll"
          ].indexOf(value) !== -1
        );
      }
    },
    dropdown: {
      type: Boolean
    }
  },
  data() {
    return {};
  },
  computed: {
    navSettings() {
      let array = ["navbar"];
      array.push(this.theme, this.type);

      return array;
    }
  }
};
</script>

<style scoped lang="scss">
@import url("https://fonts.googleapis.com/css?family=Raleway");

$breakpoints: (
  sm: 576px,
  md: 768px,
  lg: 992px,
  xl: 1140px
) !default;

$mobile-width: 640px;

@mixin mobile {
  @media (max-width: #{$mobile-width}) {
    @content;
  }
}

$font-family: "Raleway", sans-serif;

$margin: 0.5rem;
$padding: 0.5rem;

%border {
  border: 1px solid grey;
}

%base {
  font-family: $font-family;
  a {
    text-decoration: none;
  }
}

#navbar {
  @extend %base;
  padding: 0 0.25rem;
  display: grid;

  grid-template-rows: 2.5rem;
  grid-template-columns: auto 1fr;
  gap: 0.25rem;

  .nav-container {
    border: 1px solid salmon;
    align-self: center; // Vertically center
  }
  .navbar-brand {
    @extend %border;
    font-weight: bold;
  }

  .nav-links {
    a {
      margin-right: 0.25rem;
      background: rgb(180, 180, 179);

      &:last-child {
        margin-right: 0;
        background: pink;
      }
    }
  }
}

// Nav layout classes
.space-between {
  justify-items: end;
}
.space-evenly .nav-links {
  display: flex;
  justify-content: space-around;
}

.default {
  background: dodgerblue;
  a {
    color: black;
  }
}
.light {
  background: white;
  a {
    color: black;
  }
}

.dark {
  background: black;
  a {
    color: white;
  }
}
</style>
