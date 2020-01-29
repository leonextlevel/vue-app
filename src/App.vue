<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <v-app-bar-nav-icon></v-app-bar-nav-icon>

      <v-toolbar-title>Notas</v-toolbar-title>

      <v-spacer></v-spacer>

      <v-btn icon>
        <v-icon>mdi-magnify</v-icon>
      </v-btn>
    </v-app-bar>

    <v-content>
      <ListaNotas/>
    </v-content>
  </v-app>
</template>

<script>
import ListaNotas from './components/ListaNotas'

export default {
  name: 'App',

  components: {
    ListaNotas
  },

  data: () => ({
    //
  })
}
</script>
