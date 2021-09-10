<template>
  <Header />
  <Search @search="handleSearch" />
</template>

<script>
import Header from "./components/Header.vue";
import Search from "./components/Search.vue";
export default {
  name: "App",
  components: {
    Header,
    Search,
  },

  methods: {
    handleSearch(event, value) {
      console.log(event, value);
    },
  },

  mounted() {
    fetch("https://api.github.com/users/octocat")
      .then((res) => res.json())
      .then((dev) => console.log(dev))
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
}

body {
  background: var(--background-color);
  margin: 0;
}

#app {
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
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
