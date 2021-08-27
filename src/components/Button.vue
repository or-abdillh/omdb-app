<template>
   <section class="button-bookmark">
      <div class="button-bookmark-wrapper">
         <button 
         :disabled="isBookmark"
         @click="pushToBookmark" 
         class="button-bookmark-main" type="button">
            <template v-if="isBookmark" >
               Saved
            </template>
            <template v-else >
               Bookmark
            </template>
         </button>
         <button class="button-share" type="button">
            <i class="fa fa-share" ></i>
         </button>
      </div>
   </section>
   <pre>
      {{ test }}
   </pre>
</template>

<script>
   
   export default {
      name: 'Button',
      data() {
         return {
            movie: {},
            test: '',
            isBookmark: false,
         }
      },
      inheritAttrs: false,
      props: {
         detailsMovie: {
            type: Object
         }
      },
      methods: {
         pushToBookmark() {
            let local = localStorage.getItem('listBookmark_omdb')
            let movie = this.movie
            let details = this.detailsMovie
            
            movie.Poster = details.Poster
            movie.Title = details.Title,
            movie.Year = details.Year,
            movie.Type = details.Type
            movie.IdMovie = details.IdMovie
             
            if (local) {
               local = JSON.parse(local);
               local.bookmark.push(movie)
               
               if ( !this.isDuplicate(local, movie)) {
                  localStorage.setItem('listBookmark_omdb', JSON.stringify(local))
               }
               
            } else {
               local = { bookmark: []}
               local.bookmark.push(movie)
               localStorage.setItem('listBookmark_omdb', JSON.stringify(local))
            }
            
            this.isBookmark = true
            
         },
         isDuplicate(local, movie) {
            for ( const item of local.bookmark) {
               if ( item.IdMovie == movie.IdMovie ) return true
            }
            return false
         }
      },
      watch: {
         detailsMovie(val) {
            let local = JSON.parse(localStorage.getItem('listBookmark_omdb'))
            let details = this.detailsMovie
            console.log('watchers')
            
            if (local) {
               if ( this.isDuplicate(local, details)) {
                  this.isBookmark = true
               }
            }
         }
      },
      mounted() {
         console.log('mounted')
         let local = JSON.parse(localStorage.getItem('listBookmark_omdb'))
         let id = this.$route.params.idMovie
         
         console.log(local.bookmark)
         console.log(id)
         
         if (local) {
            for ( const item of local.bookmark ) {
               if ( item.IdMovie == id ) this.isBookmark = true
            }
         }
         
      }
   }
   
</script>

<style lang="scss">
   
   @import './src/scss/_button';
   
</style>