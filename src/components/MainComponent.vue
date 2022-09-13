<template>
  <main class="container">
    <h2 v-if="moviesComputed.length">FILM:</h2>
    <ul class="wrapper">
      <li class="card" v-for="(movie) in moviesComputed" :key="movie.id" @mouseenter="getActors(movie.id)">
        <div>

          <img class="card-img" :src="imgFirstPath +'w342' + movie.poster_path" :alt="movie.title"
            @error="imageLoadOnError">

        </div>
        <div class="card-img-2">
          <p>Titolo: {{movie.title}}</p>
          <p>Titolo Originale: {{movie.original_title}} </p>
          Attori: <span v-for="(actor, index) in movieActors" :key="index + 700000">
            {{actor}},
          </span>
          <p>
            Voto:
            <span v-for="(emptystar,index) in voteTransformer(movie.vote_average)" :key="emptystar + index + 50"><svg
                xmlns="http://www.w3.org/2000/svg" height="15" fill="yellow" viewBox="0 0 576 512">
                <!--! Font Awesome Pro 6.2.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. -->
                <path
                  d="M316.9 18C311.6 7 300.4 0 288.1 0s-23.4 7-28.8 18L195 150.3 51.4 171.5c-12 1.8-22 10.2-25.7 21.7s-.7 24.2 7.9 32.7L137.8 329 113.2 474.7c-2 12 3 24.2 12.9 31.3s23 8 33.8 2.3l128.3-68.5 128.3 68.5c10.8 5.7 23.9 4.9 33.8-2.3s14.9-19.3 12.9-31.3L438.5 329 542.7 225.9c8.6-8.5 11.7-21.2 7.9-32.7s-13.7-19.9-25.7-21.7L381.2 150.3 316.9 18z" />
              </svg></span>
            <span v-for="(star,index) in (maxVote - voteTransformer(movie.vote_average))"
              :key="star + index + 1500"><svg xmlns="http://www.w3.org/2000/svg" height="15" fill="yellow"
                viewBox="0 0 576 512">
                <!--! Font Awesome Pro 6.2.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. -->
                <path
                  d="M287.9 0C297.1 0 305.5 5.25 309.5 13.52L378.1 154.8L531.4 177.5C540.4 178.8 547.8 185.1 550.7 193.7C553.5 202.4 551.2 211.9 544.8 218.2L433.6 328.4L459.9 483.9C461.4 492.9 457.7 502.1 450.2 507.4C442.8 512.7 432.1 513.4 424.9 509.1L287.9 435.9L150.1 509.1C142.9 513.4 133.1 512.7 125.6 507.4C118.2 502.1 114.5 492.9 115.1 483.9L142.2 328.4L31.11 218.2C24.65 211.9 22.36 202.4 25.2 193.7C28.03 185.1 35.5 178.8 44.49 177.5L197.7 154.8L266.3 13.52C270.4 5.249 278.7 0 287.9 0L287.9 0zM287.9 78.95L235.4 187.2C231.9 194.3 225.1 199.3 217.3 200.5L98.98 217.9L184.9 303C190.4 308.5 192.9 316.4 191.6 324.1L171.4 443.7L276.6 387.5C283.7 383.7 292.2 383.7 299.2 387.5L404.4 443.7L384.2 324.1C382.9 316.4 385.5 308.5 391 303L476.9 217.9L358.6 200.5C350.7 199.3 343.9 194.3 340.5 187.2L287.9 78.95z" />
              </svg></span>
          </p>
          <p>Lingua : {{movie.original_language}} <img :src="imgSrc + language(movie.original_language)" width="30"
              :alt="movie.original_language">
          </p>
          <p>
            Anno: {{movie.release_date}}
          </p>

          <p> Overview: {{movie.overview}} </p>

        </div>

      </li>

    </ul>
    <h2 v-if="tvShowsComputed.length">SERIE TV:</h2>
    <ul class="wrapper">
      <li class="card" v-for="(show) in tvShowsComputed" :key="show.id">
        <div>

          <img class="card-img" :src="imgFirstPath +'w342' + show.poster_path" @error="imageLoadOnError"
            :alt="show.name ">

        </div>
        <div class="card-img-2">
          <p>Titolo: {{show.name}}</p>
          <p>Titolo Originale: {{show.original_name}} </p>
          
            Voto:
            <span v-for="(emptystar) in voteTransformer(show.vote_average)" :key="emptystar + 5000"><svg
                xmlns="http://www.w3.org/2000/svg" height="15" fill="yellow" viewBox="0 0 576 512">
                <!--! Font Awesome Pro 6.2.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. -->
                <path
                  d="M316.9 18C311.6 7 300.4 0 288.1 0s-23.4 7-28.8 18L195 150.3 51.4 171.5c-12 1.8-22 10.2-25.7 21.7s-.7 24.2 7.9 32.7L137.8 329 113.2 474.7c-2 12 3 24.2 12.9 31.3s23 8 33.8 2.3l128.3-68.5 128.3 68.5c10.8 5.7 23.9 4.9 33.8-2.3s14.9-19.3 12.9-31.3L438.5 329 542.7 225.9c8.6-8.5 11.7-21.2 7.9-32.7s-13.7-19.9-25.7-21.7L381.2 150.3 316.9 18z" />
              </svg></span>
            <span v-for="(star) in (maxVote - voteTransformer(show.vote_average))" :key="star + 12000"><svg
                xmlns="http://www.w3.org/2000/svg" height="15" fill="yellow" viewBox="0 0 576 512">
                <!--! Font Awesome Pro 6.2.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license (Commercial License) Copyright 2022 Fonticons, Inc. -->
                <path
                  d="M287.9 0C297.1 0 305.5 5.25 309.5 13.52L378.1 154.8L531.4 177.5C540.4 178.8 547.8 185.1 550.7 193.7C553.5 202.4 551.2 211.9 544.8 218.2L433.6 328.4L459.9 483.9C461.4 492.9 457.7 502.1 450.2 507.4C442.8 512.7 432.1 513.4 424.9 509.1L287.9 435.9L150.1 509.1C142.9 513.4 133.1 512.7 125.6 507.4C118.2 502.1 114.5 492.9 115.1 483.9L142.2 328.4L31.11 218.2C24.65 211.9 22.36 202.4 25.2 193.7C28.03 185.1 35.5 178.8 44.49 177.5L197.7 154.8L266.3 13.52C270.4 5.249 278.7 0 287.9 0L287.9 0zM287.9 78.95L235.4 187.2C231.9 194.3 225.1 199.3 217.3 200.5L98.98 217.9L184.9 303C190.4 308.5 192.9 316.4 191.6 324.1L171.4 443.7L276.6 387.5C283.7 383.7 292.2 383.7 299.2 387.5L404.4 443.7L384.2 324.1C382.9 316.4 385.5 308.5 391 303L476.9 217.9L358.6 200.5C350.7 199.3 343.9 194.3 340.5 187.2L287.9 78.95z" />
              </svg></span>
          
          <p>Lingua : {{show.original_language}} <img :src="imgSrc + language(show.original_language)" width="30"
              :alt="show.original_language"></p>
          <p>
            Anno: {{show.first_air_date}}
          </p>
          <p> Overview: {{show.overview}} </p>

        </div>

      </li>

    </ul>


  </main>
</template>
<script>
import state from '../store.js'
import axios from 'axios';

export default {
  name: 'MainComponent',
  computed: {
    moviesComputed() {
      console.log("film", state.movies)
      return state.movies
    },
    tvShowsComputed() {
      console.log("tv shows", state.tvShows)
      return state.tvShows
    }
  },
  data() {
    return {
      imgSrc: "https://countryflagsapi.com/svg/",
      imgFirstPath: 'https://image.tmdb.org/t/p/',
      maxVote: 5,
      movieActors : [],

    }
  },
  methods: {
    language(lang) {
      if (lang === "en" || lang === "EN") {
        return "gb"
      } else if (lang === "ko" || lang === "KO") {
        return "kr"
      } else {
        return lang
      }
    },
    voteTransformer(x) {
      return Math.round(x / 2)

    },
    imageLoadOnError(e) {
      e.target.src = "https://prod-spinneys-cdn.azureedge.net/static/img/no-image-found.b1edc35f0fa6.png"
    },
    getActors(id) { 
        axios
        .get(`https://api.themoviedb.org/3/movie/${id}/credits?api_key=8cbfe3a39283c4f44f68376b0e0e6c1b&language=en-US`)
        .then((res) =>{
          this.movieActors = []
          for (let i = 0; i < 5; i++) {
            this.movieActors.push(res.data.cast[i].name)
            
          }
          return this.movieActors
            
          
         
        });

    }



  },
  watch: {
    moviesComputed: function() {
      this.getActors()
    }
  },



}
</script>
<style scoped lang="scss">
@import '../index.scss';

.wrapper {
  display: grid;
  grid-template-columns: repeat(4, 1fr);


  & .card {
    width: 342px;
    display: block;

    & .card-img {
      width: 342px;
      height: 513px;

    }

    & .card-img:hover {
      display: none;
    }

    & .card-img-2 {
      background-color: rgba(0, 0, 0, 0.616);
      width: 342px;
      height: 513px;
      padding: 30px 10px;
      overflow-y: hidden;
      color: white;
      font-size: 1.5rem;
      


      & p {
        color: white;
        font-size: 1.5rem;
        margin-bottom: 5px;
      }
    }
  }
}

h2 {
  color: white;
  font-size: 40px;
  margin-bottom: 30px;
  text-align: center;
}

li {
  margin: 1rem;
  position: relative;
  width: 342px;
  height: 487px;
  overflow-y: hidden;
}
</style>