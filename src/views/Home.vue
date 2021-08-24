<template>
   <section id="header-home">
      <div class="brand">
         <strong>OMDB</strong>
         <span class="bookmark">
            <img src="src/assets/bookmark-64.png"/>
            <span>4</span>
         </span>
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
            type="text" placeholder="Type title here" />
            <button @click="getData" type="button">
               <i class="fa fa-search" ></i>
            </button>
         </div>
      </div>
      <!-- Categorys -->
      <div class="category-wrapper">
         <strong>Categorys</strong>
         <div class="badge-wrapper">
            <template v-for="item in categorys" :key="item.id">
               <div 
               @click="badgeActive = item.name" 
               :class="badgeActive === item.name ? 'active' : ''"
               class="badge"> 
                  <img src="src/assets/take-board-64.png" alt="" />
                  <p>{{ item.name }}</p>
               </div>
            </template>
         </div>
      </div>
      
      <EmptyState :show-empty-state="showEmptyState" :is-empty-state="isEmptyState" ></EmptyState>
      
      <!-- Card components -->
      <div v-if="response" class="card-wrapper">
         <strong>Search results for '{{ keyWord }}'</strong>
         <template v-for="item in response" :key="item.imdbID">
            <Card :title="item.Title" :poster="item.Poster" :year="item.Year" :type="item.Type" ></Card>
         </template>
      </div>
   </section>
</template>

<script>

   import axios from 'axios'
   import Card from '../components/Card.vue';
   import EmptyState from '../components/EmptyState.vue';
   
   export default {
      name: 'Home',
      data() {
         return {
            categorys: [
               {name: 'Movie', id: 1},
               {name: 'Episode', id: 2},
               {name: 'Series', id: 3}
            ],
            badgeActive: 'Movie',
            keyWord: '',
            response: '',
            responseStatus: 'true',
            isEmptyState: true,
            showEmptyState: true
         }
      },
      components: {
         Card,
         EmptyState
      },
      watch: {
        responseStatus(val) {
           if ( val === 'False' ) {
              this.isEmptyState = false;
              this.showEmptyState = true;
           }  
           else this.showEmptyState = false
        } 
      },
      methods: {
         getData() {
            axios.
               get('./response.json')
                  .then( res =>  {
                     this.response = res.data.Search
                     this.responseStatus = res.data.Response
                     })
                  .catch( err => this.response = err)
         }
      }
   }

</script>

<style lang="scss">
   
   @import './src/scss/view-styles/_home';
   
</style>