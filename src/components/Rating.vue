<template>
   <div class="rating">
      <small>{{ rate }}</small>
      <span class="stars">
         <template v-for="star in starArr" :key="star">
            <i :class="setStarIcon(star)" ></i>
         </template>
      </span>
   </div>
</template>

<script>
   
   export default {
      name: 'Rating',
      data() {
         return {
            starArr: []
         }
      },
      props: {
         rate: {
            type: Number,
            default: 0
         }
      },
      watch: {
         rate(val) {
            let maxStar = 5
            let mainNum = val * .5
            let lowerNum = parseInt(mainNum)
            let upperNum = lowerNum + 1
            
            this.pushStarVal('full', lowerNum)
            maxStar = maxStar - lowerNum
            
            if ( mainNum > lowerNum && mainNum < upperNum) {
               this.pushStarVal('half', 1)
               maxStar = maxStar - 1
            }
            
            this.pushStarVal('empty', maxStar)
         }
      },
      methods: {
         pushStarVal(str, N) {
            for ( let i = 1; i <= N; i++ ) {
               this.starArr.push(str)
            }
         },
         setStarIcon(str) {
            if (str === 'full') return 'fas fa-star'
            else if (str === 'half') return 'fas fa-star-half'
            else return 'far fa-star'
         }
      }
   }
   
</script>

<style lang="scss">
   
   @import './src/scss/_variabels';
   @import './src/scss/_mixins';
   
   .rating {
      
      small {
         @include poppins-style(600, rgba($text-secondary, .85));
         margin-right: .25rem;
         font-size: .6rem;
      }
      
      .stars {
         i {
            font-size: .55rem;
            color: $text-icon;
         }
      }
   }
   
</style>