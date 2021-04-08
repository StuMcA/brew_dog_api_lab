<template>
  <li>{{beer.name}}</li>
</template>

<script>

export default {
  name: 'beer-item',

  props: ['beer'],
  
  methods: {
      handleClick: function() {
        eventBus.$emit('send-beer', this.selectedBeer)
  },
},

}

</script>

<style scoped>
 li {
   list-style: none;
 }
</style>