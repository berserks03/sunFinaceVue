<template>
  <div id="app">
    <Search />
  </div>
</template>

<script lang="ts">
import Vue from 'vue';
import Search from '@/components/CitiesSearch.vue';

export default Vue.extend({
  name: 'App',
  components: {
    Search,
  },
});
</script>

<style lang="scss">
body {
  margin: 0;
  padding: 0;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  padding-top: 60px;
  box-sizing: border-box;
  position: relative;
  width: 100vw;
  min-height: 100vh;
  overflow: hidden;
}
</style>
