<template>
  <fetchApi></fetchApi>
</template>

<script>
import fetchApi from './components/fetchApi.vue';
export default {
  name: 'App',
  components: {
    fetchApi,
  }
}
</script>

<style>
body {
  margin: 0;
  padding: 0; 
  box-sizing: border-box;
}
#app {
  font-family: 'montserrat',sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
