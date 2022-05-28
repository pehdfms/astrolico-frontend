<template>
  <v-card class="mx-auto" max-width="800">
    <a :href="apod.hdurl">
      <v-img class="align-end text-white" height="400" :src="apod.url" cover>
        <v-card-title>{{ apod.title }}</v-card-title>
      </v-img>
    </a>
    <v-card-subtitle class="pt-5">{{apod.date}}</v-card-subtitle>
    <v-card-text>{{apod.explanation}}</v-card-text>
  </v-card>
</template>

<script>
export default {
  name: "APODCard",
  props: {
    apod: Object
  }
}
</script>

<style scoped>

a {
  text-decoration: none;
}

</style>