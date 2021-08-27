<template>
   <section class="nav">
      <div @click="$router.go(-1)" class="nav-back">
         <i class="fa fa-chevron-left" ></i>
         <strong>Back</strong>
      </div>
      <strong class="nav-title">
         {{ navName }}
      </strong>
   </section>
</template>

<script>
   
   export default {
      name: 'Nav',
      inheritAttrs: false,
      props: {
         navName: {
            type: String
         }
      }
   }
   
</script>

<style lang="scss">
   
   @import "./src/scss/_nav";
   
</style>