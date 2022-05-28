<template>
  <v-app>
    <v-app-bar>
      <h1>Astrolico</h1>
    </v-app-bar>
    <v-main>
      <APODList/>
    </v-main>
  </v-app>
</template>

<script>
import APODList from "@/components/APODList";

export default {
  name: 'App',

  components: {
    APODList,
  },

  data: () => ({
    //
  }),
}
</script>
