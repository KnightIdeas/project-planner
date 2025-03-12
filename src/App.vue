<template>
  <Navbar />
  <router-view/>
</template>

<script>
import Navbar from './components/Navbar.vue';

export default {
  components: { Navbar },
  mounted() {
    console.log("Bin ID:", process.env.VUE_APP_JSONBIN_ID);
console.log("Secret:", process.env.VUE_APP_JSONBIN_MASTER_KEY);
console.log("Secret:", process.env.VUE_APP_JSONBIN_ACCESS_KEY);

  }
}

</script>

<style>
body {
  background: #f2f2f2;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  max-width: 600px;
  margin: 0 auto;
  color: #555;
}

</style>
