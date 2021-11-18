<template>
  <div  id="app" class="container ">

      <tableMovies/>
      <filterMovies/>

    
  </div>
</template>

<script>
import filterMovies from './components/filterMovies.vue'
import tableMovies from './components/TableMovies.vue'


export default {
  name: 'app',
  components: {
    filterMovies,
    tableMovies
  }
}
</script>

<style>

</style>
