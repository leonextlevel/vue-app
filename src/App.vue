<template>
  <v-app>
    <v-app-bar
      app
      color="primary"
      dark
    >
      <v-spacer></v-spacer>
      <v-toolbar-title>NOTAS</v-toolbar-title>
      <v-spacer></v-spacer>
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
