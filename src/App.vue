<template>
  <div id="app">
    <List/>
  </div>
</template>

<script>
import List from './components/list.vue'
export default {
  name: 'App',
  components: {
    List
  }
}
</script>

<style>
  #app {
    font-family: Roboto, sans-serif;
    text-align: center;
    padding: 20px;
    background-color: beige;
  }
</style>