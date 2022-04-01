<template>
  <div id="app">
    <Header />
    <Main />
  </div>
</template>

<script>
import 'bootstrap/dist/css/bootstrap.css';

import Main from './components/Main.vue';
import Header from './components/Header.vue';

export default {
  name: 'App',
  components: {
    Main,
    Header
  }
}
</script>

<style lang="scss">

</style>
