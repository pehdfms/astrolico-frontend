<template>
    <li v-for="planet in results?._embedded?.planets" :key="planet.id">
      <p>{{planet}}</p>
    </li>
</template>

<script>
export default {
  name: "APODList",
  data() {
    return {
      results: results
    }
  }
}

import { ref, watchEffect } from 'vue'

const API_URL = 'http://localhost:8080/planets'

const results = ref({})

watchEffect(async () => {
  results.value = await (await fetch(API_URL)).json()
  console.log(results.value)
})

</script>

<style scoped>

</style>