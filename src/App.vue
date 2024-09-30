<template>
  <div id="app">
    <NavbarComp />
    <div class="container">
      <router-view />
    </div>
    <FooterComp />
  </div>
</template>

<script>
import NavbarComp from './components/NavbarComp.vue';
import FooterComp from './components/FooterComp.vue';

export default {
  components: {
    NavbarComp,
    FooterComp
  }
};
</script>

<style>
#app {
  background-color: black;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

.container {
  min-height: 100vh;
  max-width: 100%;
  margin: auto 0;
}

nav {
  padding: 30px;
}
</style>
