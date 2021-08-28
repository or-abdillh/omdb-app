<template>
   <section id="header-home">
      <div class="brand">
         <strong>OMDB</strong>
         <router-link to="/bookmark" class="bookmark">
            <img src="https://dl.dropbox.com/s/s9fb1d9vughng58/bookmark-64.png?dl=2"/>
            <span>{{ bookmarkCount }}</span>
         </router-link>
      </div>
      <div class="intro">
         <h3>
            Find your 
            <br>
            favorite movies
         </h3>
      </div>
      <!-- Search bar -->
      <div class="search-wrapper">
         <div class="search-bar">
            <input 
            v-model="keyWord"
            v-on:keyup.enter="getData"
            type="text" placeholder="Type title here" />
            <button @click="getData" type="button">
               <i class="fa fa-search" ></i>
            </button>
         </div>
      </div>
      <!-- Categorys -->
      <div class="category-wrapper">
         <strong>Categories</strong>
         <div class="badge-wrapper">
            <template v-for="item in categorys" :key="item.id">
               <div 
               @click="badgeClick(item.name)" 
               :class="badgeActive === item.name ? 'active' : ''"
               class="badge"> 
                  <img src="https://dl.dropbox.com/s/g35eijyruta8sv9/take-board-64.png?dl=2" alt="" />
                  <p>{{ item.name }}</p>
               </div>
            </template>
         </div>
      </div>
      
      <EmptyState :isLoad="isLoad" :show-empty-state="showEmptyState" :is-empty-state="isEmptyState" ></EmptyState>
      
      <!-- Card components -->
      <div v-if="response && !isLoad" class="card-wrapper">
         <strong>Search results for '{{ keyWordText }}'</strong>
         <template v-for="item in response" :key="item.imdbID">
            <Card :title="item.Title" :poster="item.Poster" :id-movie="item.imdbID" :year="item.Year" :type="item.Type" ></Card>
         </template>
      </div>
   </section>
</template>

<script>
   import axios from 'axios'
   import Card from '../components/Card.vue'
   import EmptyState from '../components/EmptyState.vue'
   import API from '../apiKey.js'
   
   export default {
      name: 'Home',
      data() {
         return {
            categorys: [
               {name: 'Movie', id: 1},
               {name: 'Episode', id: 2},
               {name: 'Series', id: 3}
            ],
            bookmarkCount: 0,
            badgeActive: 'Movie',
            keyWord: '',
            keyWordText: '',
            response: '',
            responseStatus: 'true',
            isEmptyState: true,
            showEmptyState: true,
            isLoad: false,
            errorMsg: null,
            key: API.omdb.key,
            endPoint: API.omdb.endPoint
         }
      },
      components: {
         Card,
         EmptyState
      },
      watch: {
        responseStatus(val) {
           if ( val === 'False' ) {
              this.isEmptyState = false
              this.showEmptyState = true
           }  
           else this.showEmptyState = false
        } 
      },
      mounted(){
        if ( localStorage.getItem('listMovie_omdb') ) {
           this.response = JSON.parse(localStorage.getItem('listMovie_omdb'))
           this.responseStatus = 'True'
           this.keyWordText = localStorage.getItem('lastKeyWord_omdb')
        }
        
        if ( localStorage.getItem('listBookmark_omdb') ) {
           let bookmark = JSON.parse(localStorage.getItem('listBookmark_omdb')).bookmark
           this.bookmarkCount = bookmark.length
        }
      },
      methods: {
         getData() {
            const validKeyWord = this.keyWord.split(' ').join('+')
            if (validKeyWord.split('').length > 0) {
               
               this.showLoader(true)
               axios.
                  get(`${this.endPoint}?apikey=${this.key}&s=${validKeyWord}&type=${this.badgeActive}`)
                     .then( res =>  {
                        this.response = res.data.Search
                        this.responseStatus = res.data.Response
                        this.keyWordText = this.keyWord
                        
                        this.showLoader(false)
                        
                        if (this.responseStatus === 'True') {
                           localStorage.setItem('listMovie_omdb', JSON.stringify(res.data.Search))
                           localStorage.setItem('lastKeyWord_omdb', this.keyWord)
                        }
                        
                        })
                     .catch( err => this.errorMsg = err)
            }
         },
         showLoader(show) {
            if (show) {   
               this.showEmptyState = true
               this.isLoad = true
            } else {
               this.showEmptyState = false
               this.isLoad = false
            }   
         },
         badgeClick(name) {
            this.badgeActive = name
            this.getData()
         }
      }
   }
</script>

<style lang="scss">
   
   @import './src/scss/view-styles/_home';
   
</style>
