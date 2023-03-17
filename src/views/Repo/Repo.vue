<template>
  <div v-if="repo" class="home">
    <h1>Repo Details</h1>
    <div class="details">
      <p><span class="bold">REPO NAME;</span> {{ id }}</p>
      <p><span class="bold">REPO FULL-NAME;</span> {{ repo.full_name }}</p>
      <p><span class="bold">REPO DESCRIPTION;</span> {{ repo.description }}</p>
      <p><span class="bold">DATE CREATED;</span> {{ repo.created_at }}</p>
      <p><span class="bold">LANGUAGE;</span> {{ repo.language }}</p>
      <p><span class="bold">VISIBILITY;</span> {{ repo.visibility }}</p>
    </div>

    <button @click="back">Go back</button>
    <button @click="redirect">Back Home</button>
  </div>
  <div v-else>
    <p>Loading Repository...</p>
  </div>
</template>

<script>
export default {
  props: ["id"],
  data() {
    return {
      repo: null,
    };
  },
  mounted() {
    fetch("https://api.github.com/repos/steelyomi/" + this.id)
      .then((res) => res.json())
      .then((data) => (this.repo = data))
      .catch((err) => console.log(err.message));
  },
  methods: {
    back() {
      this.$router.go(-1);
    },
    redirect() {
      this.$router.push({ name: "Home" });
    },
  },
};
</script>

<style>
.home .details {
  text-align: left;
  margin-left: 25px;
  font-family: "Trebuchet MS", "Lucida Sans Unicode", "Lucida Grande",
    "Lucida Sans", Arial, sans-serif;
  font-weight: 700;
}

.home .details span {
  color: crimson;
}
</style>
