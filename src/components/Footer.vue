<template>
  <div id="footer">
      <router-link class="footer-link" to="/">Home</router-link>
      <router-link class="footer-link" to="/about">About</router-link>
  </div>
</template>

<script>
export default {
    name: "Footer"
}
</script>

<style scoped>
#footer {
  width: 100vw;
  padding: 10px 0;
  text-align: center;
  background-color: #353535;
}

.footer-link {
  display: inline-block;
  color: #fff;
  margin: 0 15px;
}
</style>