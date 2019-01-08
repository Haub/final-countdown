<template>
  <div id="search">
    <div v-for="artRecord in artRecords">
      <img v-bind:src="artRecord.primaryimageurl" />
      <h3 v-for="person in artRecord.people">{{person.name}}</h3>
      <h3>{{artRecord.title}}</h3>
      <h4>{{artRecord.dated}}</h4>
      <h4>{{artRecord.displayName}}</h4>
      <h4>{{artRecord.culture}}</h4>
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
      })  
  }
}
</script>

<style scoped>
  img {
    width: 450px;
    height: 600px;
  }

</style>
