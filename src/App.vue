<template>
  <div id="app">
    <h2>Meditative Art of the Day</h2>
    <h6>From the Harvard Art Museum</h6>
    <Search/>
  </div>
</template>

<script>
import Search from './components/Search'

export default {
  name: 'App',
  components: {
    Search
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
h2 {
  font-size: 50px;
  margin-bottom: 0;
}
h6 {
  font-size: 20px;
}
</style>
