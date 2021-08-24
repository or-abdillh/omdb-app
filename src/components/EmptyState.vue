<template>
   <div v-if="showEmptyState" class="state-wrapper">
      <div v-if="isEmptyState" class="content">
         <strong>Search results will be displayed here</strong>
         <router-link to="/bookmark" class="button-to-bookmark" >
            To bookmark
         </router-link>
      </div>
      <div v-if="!isEmptyState" class="content">
         <strong>Sorry, movie not found</strong>
      </div>
   </div>
</template>

<script>
   
   export default {
      name: 'EmptyState',
      props: {
         isEmptyState: {
            type: Boolean,
            default: true
         },
         showEmptyState: {
            type: Boolean,
            default: true
         }
      }
   }
   
</script>

<style lang="scss" >
   
   @import './src/scss/_variabels';
   @import './src/scss/_mixins';
   
   .state-wrapper {
      @include padding-app;
      @include flex-centering;
      width: 100%;
      text-align: center;
      margin-top: 3rem;
      
      strong {
         @include poppins-style(400, $text-secondary);
         font-size: .7rem;
         display: block;
      }
      
      .button-to-bookmark {
         @include poppins-style(400, $text-secondary);
         display: block;
         width: 65%;
         text-decoration: none;
         font-size: .7rem;
         background: $bg-secondary;
         padding: .25rem;
         border-radius: 16px;
         margin: .5rem auto 0;
         transition: .3s;
         
         &:active {
            border:  1pc solid $text-secondary;
         }
      }
   }
   
</style>