<template>
  <div class="header">
    <h1>devfinder</h1>
    <div class="toggle">
      <h3 class="theme">{{ theme }}</h3>
      <input @change="toggleTheme" type="checkbox" id="switch" name="mode" />
      <label for="switch">Toggle</label>
    </div>
  </div>
</template>

<script>
export default {
  name: "Header",
  mounted() {
    const initUserTheme = this.getMediaPreference();
    this.setTheme(initUserTheme);
  },

  data() {
    return {
      userTheme: "light-theme",
    };
  },

  methods: {
    setTheme(theme) {
      localStorage.setItem("user-theme", theme);
      this.userTheme = theme;
      document.documentElement.className = theme;
    },

    toggleTheme() {
      const activeTheme = localStorage.getItem("user-theme");
      if (activeTheme === "light-theme") {
        this.setTheme("dark-theme");
      } else {
        this.setTheme("light-theme");
      }
    },

    getMediaPreference() {
      const hasDarkPreference = window.matchMedia(
        "(prefers-color-scheme: dark)"
      ).matches;
      if (hasDarkPreference) {
        return "dark-theme";
      } else {
        return "light-theme";
      }
    },
  },

  computed: {
    theme() {
      let theme = this.userTheme === "light-theme" ? "LIGHT" : "DARK";
      return theme;
    },
  },
};
</script>

<style scoped>
.header {
  display: flex;
  align-items: center;
  justify-content: space-between;
  margin-bottom: 20px;
}

h1 {
  color: var(--text-color);
}

h3 {
  color: var(--text-color);
}

.toggle {
  display: flex;
  align-items: center;
}

.theme {
  margin-right: 10px;
}

input[type="checkbox"] {
  height: 0;
  width: 0;
  visibility: hidden;
}

label {
  cursor: pointer;
  text-indent: -9999px;
  width: 55px;
  height: 30px;
  background: var(--text-color);
  display: flex;
  justify-content: center;
  align-items: center;
  -webkit-border-radius: 100px;
  -moz-border-radius: 100px;
  border-radius: 100px;
  position: relative;
}

label:after {
  content: "";
  background: var(--background-color);
  width: 20px;
  height: 20px;
  -webkit-border-radius: 50%;
  -moz-border-radius: 50%;
  border-radius: 50%;
  position: absolute;
  top: 5px;
  left: 4px;
  transition: cubic-bezier(0.68, -0.55, 0.27, 01.55) 320ms;
}

input:checked + label {
  background: var(--text-color);
}

input:checked + label:after {
  left: calc(100% - 5px);
  -webkit-transform: translateX(-100%);
  -moz-transform: translateX(-100%);
  -ms-transform: translateX(-100%);
  -o-transform: translateX(-100%);
  transform: translateX(-100%);
}

@media (max-width: 480px) {
  .header {
    margin-bottom: 40px;
  }
}
</style>
