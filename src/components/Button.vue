<template>
   <section class="button-bookmark">
      <div class="button-bookmark-wrapper">
         <button class="button-bookmark-main" type="button">
            Bookmark
         </button>
         <button class="button-share" type="button">
            <i class="fa fa-share" ></i>
         </button>
      </div>
   </section>
</template>

<script>
   
   export default {
      name: 'Button'
   }
   
</script>

<style lang="scss">
   
   @import './src/scss/_button';
   
</style>