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
            starArr: [],
            info: ''
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
      },
      mounted() {
         this.info = 'watch'
         let maxStar = 5
         let mainNum = this.rate * .5
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
         
         @media only screen and (min-width: 40.063em) and (max-width: 120em) {
            font-size: 1.1rem;
            margin-right: .45rem;
         } /* min-width 641px and max-width 1024px, use when QAing tablet-only issues */
      }
      
      .stars {
         i {
            font-size: .55rem;
            color: $text-icon;
            
            @media only screen and (min-width: 40.063em) and (max-width: 120em) {
               font-size: 1.05rem;
            } /* min-width 641px and max-width 1024px, use when QAing tablet-only issues */
         }
      }
   }
   
</style>