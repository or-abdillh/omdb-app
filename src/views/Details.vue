<template>
   <Nav nav-name="Details"></Nav>
   <section class="details">
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
      <Button></Button>
   </section>
</template>

<script>
   
   import axios from 'axios'
   import Nav from '../components/Nav.vue'
   import Rating from '../components/Rating.vue'
   import Button from '../components/Button.vue'
   
   export default {
      name: 'Details',
      components: {
         Nav,
         Rating,
         Button
      },
      data() {
         return {
            data: '',
            movie: {
               Poster: '',
               Title: '',
               Year: '',
               Genre: '',
               Runtime: '',
               Rating: '',
               Plot: '',
               Production: '',
               Actors: ''
            }
         }
      },
      mounted() {
         axios.get('../../details.json')
            .then( res => {
               let movie = this.movie
               let info = res.data
               movie.Poster = info.Poster
               movie.Title = info.Title
               movie.Year = info.Year
               movie.Genre = info.Genre
               movie.Runtime = info.Runtime
               movie.Rating = info.imdbRating
               movie.Plot = info.Plot
               movie.Production = info.Production
               movie.Actors = info.Actors
            })
            .catch( err => this.data = err)
      }
   }
   
</script>

<style lang="scss">
   
   @import "./src/scss/view-styles/_details";
   
</style>