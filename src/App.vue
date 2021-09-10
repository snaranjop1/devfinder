<template>
  <Header />
  <Search @search="handleSearch" />
  <Dev :dev="dev" v-if="dev" />
</template>

<script>
import Header from "./components/Header.vue";
import Search from "./components/Search.vue";
import Dev from "./components/Dev.vue";
export default {
  name: "App",
  components: {
    Header,
    Search,
    Dev,
  },

  data() {
    return {
      dev: null,
    };
  },

  methods: {
    handleSearch(value) {
      fetch(`https://api.github.com/users/${value}`)
        .then((res) => res.json())
        .then((dev) => (this.dev = dev))
        .catch((err) => console.log(err));
    },
  },

  mounted() {
    console.log("Aqui");
    fetch("https://api.github.com/users/octocat")
      .then((res) => res.json())
      .then((dev) => (this.dev = dev))
      .catch((err) => console.log(err));
  },
};
</script>

<style>
@import url("https://fonts.googleapis.com/css2?family=IBM+Plex+Mono:wght@300;400;500;600;700&display=swap");
:root {
  /* Variables for default theme (light-mode) */
  --background-color: #f6f8ff;
  --card-background: #fefefe;
  --text-color: #4b6a9b;
  --text-alt-color: #2b3442;
  --highlight-color: #0079ff;
  --highlight-hover-color: #60abff;
}

:root.dark-theme {
  /* Variables for dark mode */
  --background-color: #141d2f;
  --card-background: #1e2a47;
  --text-color: #fefefe;
  --text-alt-color: #fefefe;
  --highlight-color: #0079ff;
  --highlight-hover-color: #60abff;
}

* {
  font-family: "IBM Plex Mono", monospace;
  margin: 0;
}

body {
  background: var(--background-color);
  margin: 0;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 730px;
  padding-top: 140px;
  margin-left: auto;
  margin-right: auto;
}

@media (max-width: 768px) {
  #app {
    max-width: 600px;
  }
}

@media (max-width: 480px) {
  #app {
    padding-top: 20px;
    max-width: 385px;
  }
}
</style>
