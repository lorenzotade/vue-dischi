<template>
  <header class="container-fluid">
    <img src="../assets/img/logo.png" alt="Logo">
  </header>
</template>

<script>
export default {
  name: 'Header'
}
</script>

<style lang="scss" scoped>
  @import '../assets/style/vars.scss';

  header {
    height: 80px;
    background-color: $header-color;
    padding: 15px 25px;
    img {
      height: 100%;
    }
  }
</style>