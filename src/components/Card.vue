<template>
   <div class="card">
      <img :src="poster" alt="poster" />
      <div class="card-footer">
         <router-link :to="'/details/' + idMovie">
            <h3>{{ title }}</h3>
         </router-link>
         <small>{{ year + " | " + type }}</small>
      </div>
   </div>
</template>

<script>
   
   export default {
      name: 'Card',
      inheritAttrs: false,
      props: {
         title: {
            type: String,
            default: 'Iron Man 3'
         },
         year: {
            type: String,
            default: '2013'
         },
         type: {
           type: String,
           default: 'Movie'
         },
         idMovie: {
            type: String
         },
         poster: {
            type: String,
            default: 'src/assets/poster.jpeg'
         }
      }
   }
</script>

<style lang="scss" >
   
   @import './src/scss/_card';
   
</style>