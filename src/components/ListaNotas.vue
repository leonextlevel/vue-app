<template>
    <v-container fluid>
      <v-row dense>
        <v-col v-for="(nota, index) in notas" :key="index" cols="12" xs="12" sm="6"  md="3">
          <v-card
            color=secondary
            dark
          >
            <v-card-title class="headline">{{ nota.titulo }}</v-card-title>

            <v-card-subtitle>{{ nota.conteudo }}</v-card-subtitle>

            <v-card-actions class="justify-end">
              <v-tooltip bottom>
                <template v-slot:activator="{ on }">
                  <v-btn text icon color="white" v-on="on">
                    <v-icon>mdi-pencil</v-icon>
                  </v-btn>
                </template>
                <span>Editar</span>
              </v-tooltip>
              <v-tooltip bottom>
                <template v-slot:activator="{ on }">
                  <v-btn text icon color="white" v-on="on">
                    <v-icon>mdi-delete</v-icon>
                  </v-btn>
                </template>
                <span>Excluir</span>
              </v-tooltip>
            </v-card-actions>
          </v-card>
        </v-col>
      </v-row>

      <v-dialog v-model="dialog" fullscreen hide-overlay transition="dialog-bottom-transition">
      <template v-slot:activator="{ on }">
        <v-btn
          dark
          fixed
          bottom
          right
          fab
          v-on="on"
        >
          <v-icon>mdi-plus</v-icon>
        </v-btn>
      </template>
      <v-card>
        <v-toolbar dark color="primary">
          <v-btn icon dark @click="dialog = false">
            <v-icon>mdi-close</v-icon>
          </v-btn>
          <v-toolbar-title>Nova Nota</v-toolbar-title>
          <v-spacer></v-spacer>
          <v-toolbar-items>
            <v-btn dark text @click="salvarNota">Salvar</v-btn>
          </v-toolbar-items>
        </v-toolbar>
        <v-form>
          <v-container>
            <v-row class="justify-center">
              <v-col
                cols="12"
                md="8"
              >
                <v-text-field
                  v-model="nota.titulo"
                  label="Título"
                  required
                ></v-text-field>
              </v-col>
              <v-col cols="12" md="8">
                <v-textarea
                  v-model="nota.conteudo"
                  label="Conteúdo"
                  required
                ></v-textarea>
              </v-col>
            </v-row>
          </v-container>
        </v-form>
      </v-card>
    </v-dialog>
    </v-container>
</template>

<script>
export default {
  name: 'ListaNotas',
  data () {
      return {
        dialog: false,
        nota: {
          titulo: null,
          conteudo: null
        },
        notas: []
      }
  },
  methods: {
    salvarNota() {
      this.notas.push({
        titulo: this.nota.titulo,
        conteudo: this.nota.conteudo
      });
      this.dialog = false;
      this.limparNota()
    },
    limparNota() {
      for(let k in this.nota) {
        this.nota[k] = null
      }
    }
  }
}
</script>
