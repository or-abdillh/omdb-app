<template>
   <Nav nav-name="Details"></Nav>
   <Waiting :is-waiting="isWaiting"></Waiting>
   <section v-if="!isWaiting" class="details">
      <div class="details-main-info">
         <img :src="movie.Poster" :alt="movie.Title" />
         <strong>{{ movie.Title }}</strong>
         <div class="details-flex" >
            <p>{{ movie.Year }} • {{ movie.Genre }} • {{ movie.Runtime }}</p>
         </div>
         <Rating :rate="parseFloat(movie.Rating)"></Rating>
      </div>
      <div class="details-opt-info">
         <p>Plot</p>
         <p>
            {{ movie.Plot }}
         </p>
         <p>Actors & Production by</p>
         <p>
            {{ movie.Actors }} • {{ movie.Production }}
         </p>
      </div>
      <Button :details-movie="movie"></Button>
   </section>
</template>

<script>
   
   import axios from 'axios'
   import Nav from '../components/Nav.vue'
   import Rating from '../components/Rating.vue'
   import Button from '../components/Button.vue'
   import Waiting from '../components/Waiting.vue'
   import API from '../apiKey.js'
   
   export default {
      name: 'Details',
      components: {
         Nav,
         Rating,
         Button,
         Waiting
      },
      data() {
         return {
            errResponse: false,
            movie: {},
            endPoint: API.omdb.endPoint,
            key: API.omdb.key,
            isWaiting: true,
         }
      },
      mounted() {
         let idMovie = this.$route.params.idMovie
         let url = `${this.endPoint}?apikey=${this.key}&i=${idMovie}`
         
         axios.get(url)
            .then( res => {
               
               let movie = this.movie
               let info = res.data
               movie.IdMovie = info.imdbID
               movie.Poster = info.Poster
               movie.Title = info.Title
               movie.Year = info.Year
               movie.Genre = info.Genre
               movie.Runtime = info.Runtime
               movie.Rating = info.imdbRating
               movie.Plot = info.Plot
               movie.Production = info.Production
               movie.Actors = info.Actors
               movie.Type = info.Type
               
               this.isWaiting = false
            })
            .catch( err => console.log(err))
      }
   }
   
</script>

<style lang="scss">
   
   @import "./src/scss/view-styles/_details";
   
</style>