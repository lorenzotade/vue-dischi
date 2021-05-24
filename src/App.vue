<template>
  <div id="app">
    <Header />
    <Main />
  </div>
</template>

<script>
// importo header e main component
import Header from '@/components/Header.vue';
import Main from '@/components/Main.vue';

export default {
  name: 'App',
  components: {
    Header,
    Main
  },
}
</script>

<style lang="scss">
// importo fogli di stile per generali e bootstrap 5
@import 'assets/style/general.scss';
@import '~bootstrap/scss/bootstrap';

</style>  
