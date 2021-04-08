<template>
  <div id="app">

    <h1>Brewdog Beers</h1>
      <div class="main-container">
        <br><br>

   <label for="beer_select">Select a Beer:</label>
        <select id="beer_select" v-model="selectedBeer">
          <option disabled value="">Select a beer</option>
          <option v-for="beer in beerList" :key="beer.id" :value="beer">{{beer.name}}</option>
        </select>

        <br><br>

        <!-- Original Beer List (full) -->
        <!-- <beer-list :beerList="beerList"></beer-list> -->

        <!-- Beer details info -->
        <beer-details :beer="selectedBeer" v-if="selectedBeer"></beer-details>
        <button @click="addToFavourites">Add to favourites</button>
        <favourite-beers :favouriteBeers="favouriteBeersList"></favourite-beers>

        <!-- Example from countries of favs list -->
        <!-- <button v-if="!favouriteCountries.includes(selectedCountry)" v-on:click="addToFavourites">Add Country</button>
        <favourite-countries :favouriteCountries="favouriteCountries"></favourite-countries> -->

      </div>
  </div>
</template>

<script>

import {eventBus} from './main.js';

import beerList from './components/beerList.vue';
import beerDetails from './components/beerDetails.vue';
import favouriteBeers from './components/favouriteBeers.vue'

export default {
  name: 'App',

  components: {
    "beer-list": beerList,
    "beer-details": beerDetails,
    'favourite-beers': favouriteBeers,
  },

  data(){
    return {
      beerList: [],
      selectedBeer: null,
      searchedBeer: null,
      favouriteBeersList: [],
    }
  },

  methods: {
      addToFavourites: function(){
        if (!this.favouriteBeersList.includes(this.selectedBeer)) {
          this.favouriteBeersList.push(this.selectedBeer)
        }
        console.log(this.favouriteBeersList)
      },

      handleRemoveClick: function(){ eventBus.$on('new-favourite_beer-list', (newFavouriteBeerList) => {
        console.log("event triggered")
        this.favouriteBeersList = newFavouriteBeerList;
      })
    },

  },

  // async mounted() {
    //  const res = await fetch('https://api.punkapi.com/v2/beers?page=1&per_page=80');
    //  console.log(res);
    //  const data = await res.json();
    //  this.beerList = data;

  mounted() {
    fetch('https://api.punkapi.com/v2/beers?page=1&per_page=80')
    .then(res => res.json())
    .then(beerList => this.beerList = beerList)
    console.log(beerList);

    eventBus.$on('send-beer', (beer) => {
      console.log("event triggered", beer)
      this.selectedBeer = beer;
    })
    
    // eventBus.$on('new-favourite_beer-list', (newFavouriteBeerList) => {
    //       console.log("event triggered", beer)
    //       this.favouriteBeersList = newFavouriteBeerList;
    // })

  },
  
}

</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

.main-container {
  /* display: grid;
  justify-content: space-between; */
  margin: auto;
}

</style>
