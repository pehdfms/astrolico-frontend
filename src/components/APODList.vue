<template>
    <v-toolbar>
      <v-text-field
          hide-details
          single-line
          v-model="queuedQuery"
          placeholder="Search"
      >
      </v-text-field>

      <v-btn icon
         @click="search"
      >
        <v-icon>mdi-magnify</v-icon>
      </v-btn>

      <v-btn icon
         @click="reset"
      >
        <v-icon>mdi-refresh</v-icon>
      </v-btn>

    </v-toolbar>

    <v-pagination :length="results?.page?.totalPages" v-model="page"></v-pagination>

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
  methods: {
    search: function search() {
      titleQuery.value = queuedQuery.value
      page.value = 1
    },
    reset: function reset() {
      titleQuery.value = ""
      queuedQuery.value = ""
      page.value = 1
    }
  },
  data() {
    return {
      results: results,
      page: page,
      titleQuery: titleQuery,
      queuedQuery: queuedQuery
    }
  }
}

import { ref, watchEffect } from 'vue'

const API_ROOT = 'http://localhost:8080/'

const results = ref({})
const titleQuery = ref("")
const queuedQuery = ref("")
const page = ref(1)

watchEffect(async () => {
  let url = API_ROOT + "planets/search/findByTitle?title=" + titleQuery.value

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