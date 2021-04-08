<template>
  <section>
    <br>
    <img :src="beer.image_url" alt="Beer image" style="height:200px">
    <h3>Name: {{beer.name}}</h3>
    <p>Alc %: {{beer.abv}}%</p>
    <p>Tagline: {{beer.tagline}}</p>
    <p>First Brewed: {{beer.first_brewed}}</p>
    
  </section>

</template>

<script>
export default {
    name: 'beer-details',
    props: ['beer']
}
</script>

<style scoped>

</style>