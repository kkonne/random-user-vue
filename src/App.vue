<template>
  <div id="app">
    <nav role="navigation">
      <Navbar />
    </nav>
    
    <div class="container">
      <router-view/>
    </div>

    <Footer />
  </div>
</template>

<script>
import Navbar from "@/components/Navbar.vue";
import Footer from "@/components/Footer.vue";

export default {
  name: "App",

  components: {
    Navbar,
    Footer
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

*, *::before, *::after {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.container {
  width: 85vw;
  margin: 30px auto;
  min-height: 100vh;
}
</style>
