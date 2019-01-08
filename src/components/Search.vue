<template>
  <div id="search">
    <div v-for="artRecord in artRecords">
      <img v-bind:src="artRecord.primaryimageurl" />
    </div>
  </div>
</template>

<script>
import config from '../utilities/config.js'

export default {
  name: 'search',
  data () {
    return {
      msg: 'Search',
      artRecords: ''
    }
  },
  methods: {

  },
  mounted: function () {
    fetch(`https://api.harvardartmuseums.org/object?keyword=meditation&hasimage:0&apikey=${config.apiKey}`)
      .then(response => response.json())
      .then(results => {
        this.artRecords = results.records
        console.log(this.artRecords)
      })  
  }
}
</script>

<style scoped>

</style>
