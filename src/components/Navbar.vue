<template>
  <div id="navbar" :class="navSettings">
    <!-- Navbar Brand -->
    <a href="/">{{ brand }}</a>
    <!-- Navlinks / Dropdown-Button -->
    <button
      v-if="mobileDropdown"
      class="dropdown-button"
      @click="toggleMobileDropdown"
    >
      dropdown
    </button>
    <nav class="nav-links">
      <a v-for="(link, index) in links" :key="index" :href="link.path">
        {{ link.name }}
      </a>
    </nav>
    <nav v-if="showMobileLinks" class="mobile-dropdown-links">
      <a v-for="(link, index) in links" :key="index" :href="link.path">
        {{ link.name }}
      </a>
    </nav>
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
    mobileDropdown: {
      type: Boolean
    }
  },
  data() {
    return {
      showMobileDropdown: false
    };
  },
  computed: {
    navSettings() {
      let array = ["navbar"];
      array.push(this.theme, this.type);
      if (this.mobileDropdown) {
        array.push("has-mobile-dropdown");
      }
      return array;
    },
    showMobileLinks() {
      let show = false;
      if (this.showMobileDropdown && this.mobileDropdown) {
        show = true;
      }
      return show;
    }
  },
  methods: {
    toggleMobileDropdown() {
      this.showMobileDropdown = !this.showMobileDropdown;
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

$mobile-width: 400px;

@mixin mobile-max {
  @media (max-width: #{$mobile-width}) {
    @content;
  }
}
@mixin mobile-min {
  @media (min-width: #{$mobile-width}) {
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
    font-size: 16px;
  }
}

button {
  background: pink;
  align-self: center;
  margin: 0;
  padding: 0;
}

.navbar {
  @extend %base;
  padding: 0 0.25rem;
  display: grid;

  grid-template-rows: 2.5rem;
  grid-template-columns: auto 1fr;
  align-items: center;
  overflow: scroll;
  gap: 0.25rem;

  .navbar-brand {
    @extend %border;
    font-weight: bold;
  }

  .nav-links {
    display: flex;
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
.has-mobile-dropdown {
  display: grid;
  grid-template-columns: auto 1fr;
  .navbar-brand {
    justify-self: flex-start;
  }
  .dropdown-button {
    justify-self: flex-end;
  }
  @include mobile-min {
    .dropdown-button {
      display: none;
    }
  }
  @include mobile-max {
    .nav-links {
      display: none;
    }
  }
}

// Nav layout classes
.space-between {
  justify-items: end;
}
.space-evenly {
  .nav-links {
    justify-content: space-around;
  }
}

.mobile-dropdown-links {
  grid-column: 1 / span 3;
  display: grid;
  grid-template-rows: 1fr;
  justify-content: end;
  a {
    text-align: right;
    background: pink;
  }
  @include mobile-min {
    display: none;
  }
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
