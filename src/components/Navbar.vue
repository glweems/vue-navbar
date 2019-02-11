<template>
  <div id="navbar" :class="navSettings">
    <div class="nav-container navbar-brand">
      <a href="/" class="navbar-brand">{{ brand }}</a>
    </div>
    <nav class="nav-container nav-links">
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
      default: "",
      validator: function(value) {
        return ["", "light", "dark"].indexOf(value) !== -1;
      }
    },
    type: {
      type: String,
      default: "",
      validator: function(value) {
        return ["", "center", "space-between", "scroll"].indexOf(value) !== -1;
      }
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
$font-family: "Raleway", sans-serif;

$margin: 0.5rem;
$padding: 0.5rem;

a {
  text-decoration: none;
}

#navbar {
  background: dodgerblue;
  a {
    color: black;
  }
  width: 100%;
  display: inline-flex;
  align-items: center;
  height: 2.5rem;
  font-family: $font-family;

  .navbar-brand {
    text-align: left;
    font-weight: bold;
    display: inline-flex;
    margin: 0 $margin;
  }
  .nav-links {
    text-align: center;
    a {
      margin-right: 0.25rem;
      padding: 0 $padding;
    }
    &:last-child {
    }
  }
}

// Nav layout classes
.space-between {
  justify-content: space-between;
  .navbar-brand {
  }
}

.default {
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
