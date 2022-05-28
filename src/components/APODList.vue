<template>
    <v-toolbar>
      <v-text-field
          hide-details
          prepend-icon="mdi-magnify"
          single-line
          v-model="titleQuery"
      >
      </v-text-field>
    </v-toolbar>
    <div class="card-list">
      <div v-for="planet in results?._embedded?.planets" :key="planet.id">
        <APODCard :apod="planet"></APODCard>
      </div>
    </div>
    <v-pagination :length="results?.page?.totalPages" v-model="page"></v-pagination>
</template>

<script>
import APODCard from "@/components/APODCard";
export default {
  name: "APODList",
  components: {APODCard},
  data() {
    return {
      results: results,
      page: page,
      titleQuery: titleQuery
    }
  }
}

import { ref, watchEffect } from 'vue'

const API_ROOT = 'http://localhost:8080/'
const API_URL = API_ROOT + 'planets?size=10'

const results = ref({})
const titleQuery = ref("")
const page = ref(1)

watchEffect(async () => {
  let url = API_URL

  if (titleQuery.value) {
    url = API_ROOT + "planets/search/findByTitle?title=" + titleQuery.value + "&size=10"
  }

  url += '&page=' + (page.value - 1).toString()
  console.log(url)

  results.value = await (await fetch(url)).json()
  console.log(results.value)
})

</script>

<style scoped>

.card-list {
  display: flex;
  flex-direction: column;
  gap: 1.5rem;
  margin-top: 2rem;
}

</style>