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
      <div class="search-wrapper">
         <div class="search-bar">
            <input type="text" placeholder="Type title here" />
            <button type="button">
               <i class="fa fa-search" ></i>
            </button>
         </div>
      </div>
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
   </section>
</template>
            

<script>

   export default {
      name: 'Home',
      data() {
         return {
            categorys: [
               {name: 'Movie', id: 1},
               {name: 'Episode', id: 2},
               {name: 'Series', id: 3}
            ],
            badgeActive: 'Movie'
         }
      },
      components: {}
   }

</script>

<style lang="scss">
   
   @import './src/scss/view-styles/_home';
   
</style>