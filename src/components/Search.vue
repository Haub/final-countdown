<template>
  <div id="search">
    <div class='carousel_controls'>
      <button class='carousel_button' @click="previous">prev</button>
      <button class='carousel_button' @click="next">next</button>
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
        <h3 class='title'>{{artRecord.title}}</h3>
        <h3 v-for="person in artRecord.people">{{person.name}}</h3>
        <h4 class='date'>{{artRecord.dated}}</h4>
        <h4 class='culture'>{{artRecord.culture}}</h4>
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
      artRecords: '',
      firstArtRecord: ''
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
    fetch(`https://api.harvardartmuseums.org/object?keyword=meditation&hasimage=1&size=100&apikey=${config.apiKey}`)
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
    height: 550px;
    border: 12px solid #83B4AE;
    overflow: hidden;
  }
  .title {
    font-style: italic;
  }
  .image {
    margin-bottom: 1000px;
  }
  .carousel_controls {
    margin: 2.6em;
  }
  .carousel_button:hover {
    text-decoration: underline;
    cursor: pointer;
  }
  .carousel_button {
    outline: none;
    color: #fff;
    border-radius: 10%;
    background-color: #83B4AE;
    margin: 0 6rem;
    font-size: 1.2rem;
  }

</style>
