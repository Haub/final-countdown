<template>
  <div id="search">

  </div>
</template>

<script>
import config from '../utilities/config.js'

export default {
 name: 'search',
 data () {
   return {
     msg: 'Search'
   }
 },
 methods: {

 },
 mounted: function () {
   fetch(`https://api.harvardartmuseums.org/object?keyword=meditation&hasimage:0&apikey=${config.apiKey}`)
     .then(response => response.json())
     .then(results => console.log(results.records));
 }
}
</script>

<style scoped>

</style>
