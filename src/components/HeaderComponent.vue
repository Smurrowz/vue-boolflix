<template>

  <header class="container">
    <div class="header-left">
      <div class="header-img">
        <img src="../assets/img/netflix-logo-png-2562.png" alt="netflix logo">
      </div>
      <nav>
        <ul>
          <li><a href="#">Film</a></li>
          <li><a href="#">Serie TV</a></li>
          <li><a href="#">Anime</a></li>
          <li><a href="#">Originali Netflix</a></li>
          <li><a href="#">Home</a></li>
        </ul>
      </nav>
    </div>
    <div >
      <input class="input-text" v-model="inputText" type="text">
      <button class="input-button" @click="fetchMovies(), fetchTvShows()">
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
    },
    fetchTvShows(){
      axios
        .get(`${this.BASE_URI}/search/tv`, {
          params: {
            api_key: this.api_key,
            query: this.inputText,
          }
        })
        .then((res) => {
          state.tvShows = res.data.results
          console.log(this.tvShows)
        })
    },
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
      gap: 15px;
      & a{
        color: white;
        text-decoration: none;
      }

    }
  }

  & .input-text {
    border-radius: 8px;
    line-height: 20px;
    margin-right: 10px;

  }
  & .input-button{
    border-radius: 8px;
    line-height: 20px;
    padding: 0 10px;
    font-weight: bold;
    &:hover{
      background-color: grey;
      color: white;
    }
  }

}

.header-img {
  max-width: 150px;
  margin-right: 50px;

}
</style>