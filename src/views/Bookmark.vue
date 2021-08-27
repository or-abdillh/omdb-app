<template>
   <Nav nav-name="Bookmarks"></Nav>
   <section class="bookmark-view">
      <div v-if="isEmptyList" class="bookmark-empty">
         <strong>
            there is no item you saved here, try saving a new item
         </strong>
         <i class="far fa-sad-tear"></i>
      </div>
      <template v-if="!isEmptyList" v-for="item in listBookmarks" :key="item.IdMovie">
         <div class="bookmark-card">
            <img :src="item.Poster" alt="item.Poster" />
            <div class="bookmark-layer">
               <router-link :to="'/details/'+item.IdMovie" >{{ item.Title }}</router-link>
               <small>{{ item.Year }} | {{ item.Type }}</small>
               <i @click="deleteItem(item.IdMovie)" class="fa fa-trash" ></i>
            </div>
         </div>
      </template>
   </section>
</template>

<script>

   import Nav from '../components/Nav.vue'

   export default {
      name: 'Bookmark',
      components: {
         Nav
      },
      data() {
         return {
            listBookmarks: {},
            deleteTrig: true,
            isEmptyList: false
         }
      },
      mounted() {
         this.renderBookmark()
      },
      methods: {
         deleteItem(id) {
            let local = JSON.parse(localStorage.getItem('listBookmark_omdb'))
            local.bookmark.forEach( (item, index) => {
               if ( item.IdMovie == id ) {
                  local.bookmark.splice(index, 1)
                  localStorage.setItem('listBookmark_omdb', JSON.stringify(local))
                  this.deleteTrig = !this.deleteTrig
               }
            })
         },
         renderBookmark() {
            let local = localStorage.getItem('listBookmark_omdb')
            if (local) {
               this.listBookmarks = JSON.parse(local).bookmark
              
               if (this.listBookmarks.length == 0) {
                  this.isEmptyList = true
               }
            } else {
               this.isEmptyList = true
            }
         }
      },
      watch: {
         deleteTrig() {
            setTimeout(() => {
               this.renderBookmark()
            }, 500)
         }
      }
   }
   
</script>

<style lang="scss">
   
   @import 'src/scss/view-styles/_bookmark';
   
</style>