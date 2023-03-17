<template>
  <div class="home">
    <h1>Hi, Welcome...</h1>
    <p>
      I'm Abayomi, an aspiring front-end developer and a student of ALT School
      Africa.<br />
      This is a simple web application that keeps track and displays my GITHUB
      repositories.<br />
      Make sure to have fun with it...Cheers.
    </p>
    <router-link :to="{ name: 'Repos' }">
      <button>Click here to begin</button>
    </router-link>
  </div>
</template>

<script>
export default {
  name: "Home",
  components: {},
};
</script>

<style>
.home {
  font-family: Georgia, "Times New Roman", Times, serif;
  background-color: #ffffff;
  border-radius: 8px;
  box-shadow: 0px 4px 10px rgba(0, 0, 0, 0.4);
  padding: 20px;
  margin: auto;
  margin-bottom: 20px;
  width: 50%;
}

.home h1 {
  font-size: 28px;
  font-weight: bold;
  margin-bottom: 10px;
}

.home h2 {
  font-size: 20px;
  font-weight: bold;
  margin-bottom: 10px;
}

.home p {
  font-size: 16px;
  line-height: 1.8;
  margin-bottom: 15px;
}
</style>
