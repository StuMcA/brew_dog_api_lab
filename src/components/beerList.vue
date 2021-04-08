<template>
  <ul>
     <beer-item v-for="(beerItem, id) in beerList" :key="id" :beer="beerItem"></beer-item>
  </ul>
</template>

<script>
import beerItem from './beerItem.vue'

export default {
   name: 'beer-list',

   props: ['beerList'],

   components: {
        "beer-item": beerItem
   },
}

</script>

<style scoped>

</style>