<template>
  <div class="search-bar">
    <form class="search-form" @submit.prevent="makeSearch">
      <svg
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        class="search-icon"
        viewBox="0 0 24 24"
      >
        <path
          stroke-linecap="round"
          stroke-linejoin="round"
          stroke-width="1"
          d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
        />
      </svg>
      <input
        type="text"
        placeholder="Search GitHub username..."
        class="search-input"
        content="width=device-width, initial-scale=1, maximum-scale=1"
        v-model="search"
        required
      />
      <button type="submit" class="search-btn">Search</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "search",

  data() {
    return {
      search: "",
    };
  },

  methods: {
    makeSearch() {
      this.$emit("search", this.search);
    },
  },
};
</script>

<style scoped>
.search-bar {
  padding: 10px;
  border-radius: 15px;
  box-shadow: 0px 4px 4px 0px rgba(0, 0, 0, 0.25);
  background: var(--card-background);
}

.search-form {
  display: flex;
  align-items: center;
  height: 50px;
  width: 100%;
}

.search-icon {
  padding: 0px 10px;
  height: 35px;
  stroke: var(--highlight-color);
}

.search-input {
  -webkit-appearance: none;
  appearance: none;
  background: transparent;
  border: none;
  color: var(--text-color);
  font-size: 1.2rem;
  flex-grow: 3;
  font-weight: 400;
}

.search-input:focus-visible,
.search-input:focus {
  outline-style: none;
  outline: 0;
  border: 0;
}

.search-btn {
  height: 100%;
  width: 100px;
  border-radius: 10px;
  border: none;
  background: var(--highlight-color);
  color: #fefefe;
  font-size: 0.9rem;
  font-weight: 500;
}

.search-btn:hover {
  cursor: pointer;
  background: var(--highlight-hover-color);
}

@media (max-width: 480px) {
  .search-icon {
    padding: 0px 5px;
    height: 35px;
  }

  .search-input {
    font-size: 0.9rem;
    font-weight: 400;
  }
}
</style>
