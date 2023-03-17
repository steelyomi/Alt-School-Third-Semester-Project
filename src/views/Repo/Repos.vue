<template>
  <h1 class="repo-title">MY GITHUB REPOSITORIES</h1>
  <div v-if="repos.length">
    <div v-for="repo in displayedItems" :key="repo.id" class="repo">
      <router-link :to="{ name: 'Repo', params: { id: repo.name } }">
        <h2>{{ repo.name }}</h2>
      </router-link>
    </div>
    <div>
      <button @click="prevPage" :disabled="currentPage === 1">Previous</button>
      <button @click="nextPage" :disabled="currentPage === pageCount">
        Next
      </button>
    </div>
  </div>
  <div v-else>
    <h3>Loading Repositories</h3>
  </div>
</template>

<script>
export default {
  data() {
    return {
      repos: [],
      pageSize: 5,
      currentPage: 1,
    };
  },
  mounted() {
    fetch("https://api.github.com/users/steelyomi/repos")
      .then((res) => res.json())
      .then((data) => (this.repos = data))
      .catch((err) => console.log(err.message));
  },
  computed: {
    pageCount() {
      // calculate the total number of pages
      return Math.ceil(this.repos.length / this.pageSize);
    },
    displayedItems() {
      // return a subset of items based on the current page
      const start = (this.currentPage - 1) * this.pageSize;
      const end = start + this.pageSize;
      return this.repos.slice(start, end);
    },
  },
  methods: {
    prevPage() {
      // go to the previous page
      this.currentPage--;
    },
    nextPage() {
      // go to the next page
      this.currentPage++;
    },
  },
};
</script>

<style>
.repo-title {
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
}

.repo h2 {
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
  background: #5e5b5b;
  padding: 20px;
  border-radius: 10px;
  margin: 10px auto;
  max-width: 600px;
  cursor: pointer;
  color: #ffffff;
}

.repo h2:hover {
  background: #979797;
}

.repo a {
  text-decoration: none;
}

button {
  background-color: crimson;
  border: none;
  color: white;
  padding: 12px 24px;
  text-align: center;
  text-decoration: none;
  display: inline-block;
  font-size: 12px;
  border-radius: 6px;
  cursor: pointer;
  margin: auto 10px;
}

button:hover {
  background-color: #e98a96;
}
</style>
