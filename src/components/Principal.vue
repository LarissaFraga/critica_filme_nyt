<template>
  <v-container>
    <v-row class="text-center">
      <v-col cols="12">
        <!-- <v-img
          :src="require('../assets/logo.svg')"
          class="my-3"
          contain
          height="200"
        /> -->
      </v-col>

      <v-col class="mb-4">
        <h1 class="display-2 font-weight-bold mb-3">
          Critica Filmes New York Times
        </h1>

        <v-text-field label="Ex: Avengers" solo v-model="campoBusca">
        </v-text-field>
        <v-btn depressed color="primary" v-on:click="buscar"> Buscar </v-btn>
      </v-col>

      <v-col class="mb-5" cols="12">
        <v-row justify="center">
          <!-- v-for="(task, i) in tasks" :key="task.name" -->
          <v-card v-for="(filme,i) in listaFilmes" :key="i" class="mx-auto my-12" max-width="350">
            <template slot="progress">
              <v-progress-linear
                color="deep-purple"
                height="10"
                indeterminate
              ></v-progress-linear>
            </template>
            
            <v-img
              height="200"
              :src="filme.multimedia.src" 
              v-if="filme.multimedia != null"
            ></v-img>
            <v-card-title>{{ filme.display_title }} </v-card-title>
            <v-card-text>
              <v-row align="center" class="mx-0">
              </v-row>
              <div>
                {{ filme.headline }}
              </div>
            </v-card-text>

            <!-- <v-divider class="mx-4"></v-divider> -->
          </v-card>
        </v-row>
      </v-col>
    </v-row>
  </v-container>
</template>

<script>
import axios from "axios";

export default {
  name: "Principal",
  data() {
    return {
      campoBusca: "",
      listaFilmes: [],
    };
  },
  methods: {
    buscar() {
      if (this.campoBusca != "") {
        axios
          .get(
            "https://api.nytimes.com/svc/movies/v2/reviews/search.json?query=" +
              this.campoBusca +
              "&api-key=PF633Ah7nRRkAnXW0U0soEO5N97HblgZ"
          )
          .then((res) => {
            this.listaFilmes = res.data.results;
          });
      }
    },
  },
};
</script>
