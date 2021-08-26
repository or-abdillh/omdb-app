<template>
   <Nav nav-name="Details"></Nav>
   <section class="details">
      <div class="details-main-info">
         <img :src="movie.Poster" :alt="movie.Title" />
         <strong>{{ movie.Title }}</strong>
         <div class="details-flex" >
            <p>{{ movie.Year }} | {{ movie.Genre }} | {{ movie.Runtime }}</p>
         </div>
         <Rating :rate="parseFloat(movie.Rating)"></Rating>
      </div>
   </section>
</template>

<script>
   
   import axios from 'axios'
   import Nav from '../components/Nav.vue'
   import Rating from '../components/Rating.vue'
   
   export default {
      name: 'Details',
      components: {
         Nav,
         Rating
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
               Rating: ''
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
            })
            .catch( err => this.data = err)
      }
   }
   
</script>

<style lang="scss">
   
   @import "./src/scss/view-styles/_details";
   
</style>