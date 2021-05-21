<template>
  <div id="navbar">
          <img src="../assets/logo.svg" width="200px" class="nav-logo" alt="DEPT Logo">
  </div>
</template>

<script>
export default {
    name: "Navbar"
}
</script>

<style scoped>
#navbar {
    width: 100vw;
    text-align: center;
    padding: 10px 0 5px 0;
    border-bottom: 1px solid #000;
}

@media screen and (max-width: 768px) {
    #navbar .nav-logo {
        width: 100px;
    }
}
</style>