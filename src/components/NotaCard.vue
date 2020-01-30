<template>
    <v-container fluid>
          <v-card
            color=secondary
            dark
          >
            <v-card-title class="headline" v-show="nota">{{ nota.titulo }}</v-card-title>

            <v-card-subtitle v-show="nota">{{ nota.conteudo }}</v-card-subtitle>

            <v-card-actions class="justify-end">
              <v-tooltip bottom>
                <template v-slot:activator="{ on }">
                  <v-btn text icon color="white" v-on="on" @click="$emit('clickEditarNota', id)">
                    <v-icon>mdi-pencil</v-icon>
                  </v-btn>
                </template>
                <span>Editar</span>
              </v-tooltip>
              <v-tooltip bottom>
                <template v-slot:activator="{ on }">
                  <v-btn text icon color="white" v-on="on" @click="$emit('clickRemoverNota', id)">
                    <v-icon>mdi-delete</v-icon>
                  </v-btn>
                </template>
                <span>Excluir</span>
              </v-tooltip>
            </v-card-actions>
          </v-card>
    </v-container>
</template>

<script>
export default {
  name: 'NotaCard',
  props: {
    nota: Object,
    id: Number
  }
}
</script>
