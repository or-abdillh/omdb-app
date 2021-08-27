<template>
   <section v-if="isWaiting" class="waiting">
      <div class="waiting-box">
         <strong>Please wait, fetching data from server</strong>
         <i class="fa fa-smile-beam" ></i>
      </div>
   </section>
</template>

<script>
   
   export default {
      name: 'Waiting',
      props: {
         isWaiting: {
            type: Boolean,
            default: true
         }
      }
   }
   
</script>

<style lang="scss">
   
   @import 'src/scss/_variabels';
   @import 'src/scss/_mixins';
   
   .waiting {
      @include padding-app;
      width: 100%;
      position: absolute;
      top: 50%;
      left: 50%;
      transform: translate(-50%, -50%);
      
      .waiting-box {
         @include flex-column-centering;
         width: 50%;
         margin: 0 auto;
         strong {
            @include poppins-style(400, $text-secondary);
            text-align: center;
            font-size: .75rem;
            margin-bottom: .55rem;
         }
         
         i {
            @include padding-app;
            color: $text-secondary;
            background: $bg-secondary;
            width: 100%;
            border-radius: 8px;
            text-align: center;
         }
      }
   }
   
</style>