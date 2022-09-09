<template>
  <main>
    <ul>
      <li v-for="(movie, index) in moviesComputed" :key="movie.id">
        {{index + 1}} {{movie.original_title}} - {{movie.title}} - {{movie.original_language}} - {{movie.vote_average}} - {{movie.release_date}}
        
        
      </li>
      
    </ul>
    
  </main>
</template>
<script>
import state from '../store.js'
export default {
  name: 'MainComponent',
  computed: {
    search(){
    
      return state.input 
    },
    moviesComputed(){
      console.log(state.movies)
      return state.movies
    },
  },
  

  
}
</script>
<style scoped lang="scss">
@import '../index.scss';
li{
  color: white;
  font-size: 1.5rem;
  margin-bottom: 5px;
}
</style>