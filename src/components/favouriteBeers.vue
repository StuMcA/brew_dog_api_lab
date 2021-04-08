<template>
  <ul>
        <li v-for="(beer, id) in favouriteBeers" :key="id" :beer="beer">
          <button @click="removeBeer(beer), handleRemoveClick">Remove</button>
          {{beer.name}}
        </li>
  </ul>
</template>

<script>
import {eventBus} from '../main.js'

export default {
    name: 'favourite-beers', 
    data(){
    return {
      newFavouriteBeerList: [],
    }
  },

    props: [
        'favouriteBeers',
        // 'removeBeer'
        // 'eventBusOn'
    ],

    methods: {
      removeBeer: function(beerForRemoval){
        this.newFavouriteBeerList = this.favouriteBeers.filter(beer => beer.name !== beerForRemoval.name)
        console.log(this.favouriteBeers);
        console.log(this.newFavouriteBeerList);
        eventBus.$emit('new-favourite-beer-list', this.newFavouriteBeerList)
      },
               
    },
}

</script>

<style scoped>
 li {
   list-style: none;
   /* list-align: left; */
 }
</style>