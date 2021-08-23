<template>
  <h1>{{ msg }}</h1>

  <p>
    <a href="https://vitejs.dev/guide/features.html" >
      Vite Documentation
    </a>
    |
    <a href="https://v3.vuejs.org/" >Vue 3 Documentation</a>
  </p>

  <button type="button" @click="count++">
    count is: {{ count }}
  </button>
  <p>
    Edit
    <code>components/HelloWorld.vue</code> to test hot module replacement.
  </p>
</template>

<script>
import { defineProps, reactive } from 'vue'

export default {
   data() {
      return {
         count: 0
      }
   }
}
</script>

<style scoped>
a {
  color: #42b983;
}
</style>
