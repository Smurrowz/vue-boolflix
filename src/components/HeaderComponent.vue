<template>

  <header class="container">
    <div class="header-left">
      <div class="header-img">
        <img src="../assets/img/netflix-logo-png-2562.png" alt="netflix logo">
      </div>
      <nav>
        <ul>
          <li>bla</li>
          <li>bla</li>
          <li>bla</li>
          <li>bla</li>
          <li>bla</li>
        </ul>
      </nav>
    </div>
    <div class="header-right">
      <input v-model="inputText" type="text">
      <button @click="fetchMovies()">
        Cerca
      </button>
    </div>

  </header>


</template>
<script>
import state from '../store';
import axios from 'axios'

export default {
  name: 'HeaderComponent',
  data(){
    return{
      inputText: '',
      movies: [],
      tvShows: [],
      api_key: '8cbfe3a39283c4f44f68376b0e0e6c1b',
      BASE_URI: 'https://api.themoviedb.org/3'
    }
  },
  // watch: {
  //   input: function(){
  //     state.input = this.input
      

  //   }
  // },
  methods: {
    fetchMovies() {
      axios
        .get(`${this.BASE_URI}/search/movie`, {
          params: {
            api_key: this.api_key,
            query: this.inputText,
          }
        })
        .then((res) => {
          state.movies = res.data.results
          console.log(this.movies)
        })
    }
  },
  
}
</script>
<style scoped lang="scss">
@import '../index.scss';

 .container {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 0;

  & .header-left {
    display: flex;
    align-items: center;

    & ul {
      display: flex;
      color: white;
      gap: 15px;

    }
  }

  & .header-right {
    border-radius: 10px;
  }
}

.header-img {
  max-width: 150px;
  margin-right: 50px;

}
</style>