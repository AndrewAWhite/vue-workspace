<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <div class="d-flex align-center">
        Vuetify Query Builder
      </div>

      <v-spacer></v-spacer>

      <v-btn
        href="https://github.com/AndrewAWhite/vue-workspace"
        target="_blank"
        text
      >
        <span class="mr-2">Repo</span>
        <v-icon>mdi-open-in-new</v-icon>
      </v-btn>
    </v-app-bar>

    <v-content>
      <QueryBuilder/>
    </v-content>
  </v-app>
</template>

<script>
import QueryBuilder from './components/QueryBuilder'

export default {
  name: 'App',

  components: {
    QueryBuilder
  },

  data: () => ({
    //
  })
}
</script>
