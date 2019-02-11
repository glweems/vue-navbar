<template>
  <div id="navbar" :class="navSettings">
    <div class="nav-container navbar-brand">
      <a href="/">{{ brand }}</a>
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
      default: "default",
      validator: function(value) {
        return ["default", "light", "dark"].indexOf(value) !== -1;
      }
    },
    type: {
      type: String,
      default: "space-evenly",
      validator: function(value) {
        return (
          ["center", "space-between", "space-evenly", "scroll"].indexOf(
            value
          ) !== -1
        );
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

%border {
  border: 1px solid grey;
}

a {
  text-decoration: none;
}

#navbar {
  margin-bottom: 1rem;

  width: 100%;
  // display: inline-flex;
  align-items: center;
  height: 2.5rem;
  font-family: $font-family;

  .navbar-brand {
    @extend %border;
    text-align: left;
    font-weight: bold;
  }
  .nav-links {
    text-align: center;
    display: flex;
    margin: 0 auto;
    @extend %border;
    a {
      @extend %border;
      margin-right: 0.25rem;
      font-size: 16px;
    }
    :last-child {
      margin-right: 0;
    }
  }
}

// Nav layout classes
.space-between {
  display: grid;
  grid-template-columns: 1fr auto;
  justify-content: space-around;
  .navbar-brand {
    justify-self: start;
  }
  .nav-links {
    justify-self: flex-end;
  }
}
.space-evenly {
  display: grid;
  grid-template-columns: auto 1fr;
  grid-gap: 10px;
  .nav-links {
    justify-content: space-evenly;
    width: 100%;
    display: flex;

    a {
    }
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
