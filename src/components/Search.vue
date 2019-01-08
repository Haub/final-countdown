<template>
  <div id="search">
    <div class='carousel-controls'>
      <button class='carousel-controls__button' @click="previous">prev</button>
      <button class='carousel-controls__button' @click="next">next</button>
    </div>
    <transition-group
      class='carousel'
    >
      <div 
        v-for="artRecord in artRecords"
        class="image"
        :key="artRecord.id"
        tag="div"
      >
        <img v-bind:src="artRecord.primaryimageurl" />
        <h3 v-for="person in artRecord.people">{{person.name}}</h3>
        <h3>{{artRecord.title}}</h3>
        <h4>{{artRecord.dated}}</h4>
        <h4>{{artRecord.displayName}}</h4>
        <h4>{{artRecord.culture}}</h4>
      </div>
    </transition-group>

  </div>
</template>

<script>
import config from '../utilities/config.js';

export default {
  name: 'search',
  data () {
    return {
      msg: 'Search',
      artRecords: ''
    }
  },
  methods: {
    next () {
      const first = this.artRecords.shift()
      this.artRecords = this.artRecords.concat(first)
    },
    previous () {
      const last = this.artRecords.pop()
      this.artRecords = [last].concat(this.artRecords)
    }
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
