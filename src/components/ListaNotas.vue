<template>
    <v-container fluid>
      <v-row dense>
        <v-col
          v-for="(nota, index) in notas"
          :key="index"
          cols="12" xs="12" sm="6" md="3"
        >
          <nota-card :nota="nota" :id="index" @clickEditarNota="editarNota" @clickRemoverNota="removerNota"></nota-card>
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
        <v-container>
          <v-row class="justify-center">
            <v-col cols="12" md="8">
            <v-form
              ref="form"
              lazy-validation
              cols="12" md="8"
            >
            <v-col>
              <v-text-field
                v-model="nota.titulo"
                :rules="tituloRules"
                label="Título"
                required
              ></v-text-field>
            </v-col>
            <v-col>
              <v-textarea
                v-model="nota.conteudo"
                :rules="conteudoRules"
                label="Conteúdo"
                required
              ></v-textarea>
            </v-col>
            <v-col>
              <v-label>Cor da Nota</v-label>
              <v-radio-group
                v-model="nota.cor"
                col
                :rules="corRules"
                required
              >
                <v-radio color=blue label="Azul" value="blue"></v-radio>
                <v-radio color=red label="Vermelho" value="red"></v-radio>
                <v-radio color=yellow label="Amarelo" value="yellow"></v-radio>
                <v-radio color=green label="Verde" value="green"></v-radio>
              </v-radio-group>
            </v-col>
            </v-form>
            <v-col cols="12" md="5" sm="8" xs="12">
              <v-switch v-model="prenota" class="ma-2" label="Pré-visualizar nota"></v-switch>
              <nota-card v-if="prenota" :nota="nota"></nota-card>
            </v-col>
            </v-col>
          </v-row>
        </v-container>
      </v-card>
    </v-dialog>
    </v-container>
</template>

<script>
import NotaCard from './NotaCard.vue'

export default {
  name: 'ListaNotas',
  components: {
    NotaCard
  },
  data () {
    return {
      dialog: false,
      prenota: false,
      nota: {
        titulo: null,
        conteudo: null,
        cor: null,
      },
      notas: [],
      tituloRules: [
        v => !!v || 'Título é obrigatório'
      ],
      conteudoRules: [
        v => !!v || 'Conteúdo é obrigatório'
      ],
      corRules: [
        v => !!v || 'Cor é obrigatória'
      ]
    }
  },
  methods: {
    salvarNota () {
      let nota = {}
      nota = Object.assign(nota, this.nota)
      if (this.$refs.form.validate()) {
        if (nota.id != null && nota.id >= 0) {
          this.notas[nota.id] = nota
        } else {
          this.notas.push(nota)
        }
        this.dialog = false
        this.$refs.form.reset()
      }
    },
    editarNota (id) {
      this.nota = this.notas[id]
      this.nota.id = id
      this.dialog = true
    },
    removerNota (id) {
      this.notas.splice(id, 1)
    }
  }
}
</script>
