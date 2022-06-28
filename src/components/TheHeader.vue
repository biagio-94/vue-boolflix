<template>
  <div>
    <input type="text" v-model="testoInserito" />
    <button class="btn btn-danger" @click="uploadmyStore()">OK</button>
  </div>
</template>

<script>

import axios from "axios";
import { state } from "../store";
export default {
  data() {
    return {
      testoInserito: "",
    };
  },
 
  methods: {
    uploadmyStore() {
      if (this.testoInserito.length >= 0) {
        state.testoDaRicercare=this.testoInserito
      }
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=c47fc9efae23d89f94e602631b3ba67e&query=${this.testoInserito}`)
        .then((value)=>{
            state.testArray=value.data.results
        })
        axios.get(`https://api.themoviedb.org/3/search/tv?api_key=c47fc9efae23d89f94e602631b3ba67e&query=${this.testoInserito}`)
        .then((value)=>{
            state.testArraySeries=value.data.results
        })
      
    },
  },
};
</script>

<style lang="scss">
</style>