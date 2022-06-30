<template>
  <div class="main-background">
    <div class="container">
      <div class="row mygap">
        <h1 class="text-white">Film</h1>
        <div
          v-for="(value, i) in visualizzaArrayStore"
          :key="value + i"
          class="col-3"
        >
          <CardofDFilm :myProps="value"></CardofDFilm>
        </div>
      </div>
      <div class="row mygap mt-5">
        <h1 class="text-white">Serie TV</h1>
        <div
          v-for="(value, i) in visualizzaArrayStoreSerieTV"
          :key="value + i"
          class="col-3"
        >
          <CardofSeries :myProps="value"></CardofSeries>
        </div>
      </div>
    </div>
  
  </div>
</template>

<script>
import CardofDFilm from "../components/CardofFilm.vue";
import CardofSeries from "../components/CardofSeries.vue";
import axios from "axios";
import { state } from "../store";
export default {
  components: {
    CardofDFilm,
    CardofSeries,
  },
  data() {
    return {
      testoInserito: "",
    };
  },
  mounted() {
    axios
      .get(
        `https://api.themoviedb.org/3/search/movie?api_key=c47fc9efae23d89f94e602631b3ba67e&query=${state.testoDaRicercare}`
      )
      .then((value) => {
        state.testArray = value.data.results;
      });
    axios
      .get(
        `https://api.themoviedb.org/3/search/tv?api_key=c47fc9efae23d89f94e602631b3ba67e&query=${state.testoDaRicercare}`
      )
      .then((value) => {
        state.testArraySeries = value.data.results;
      });
  },
  computed: {
    visualizzaArrayStore() {
      return state.testArray;
    },
    visualizzaArrayStoreSerieTV() {
      return state.testArraySeries;
    },
  },
  methods: {
    
  },
  /*  watch:{
    testoInserito: function(){
      axios.get(`https://api.themoviedb.org/3/search/movie?api_key=c47fc9efae23d89f94e602631b3ba67e&query=${state.testoDaRicercare}`)
        .then((value)=>{
            state.testArray=value.data.results
        })
        axios.get(`https://api.themoviedb.org/3/search/tv?api_key=c47fc9efae23d89f94e602631b3ba67e&query=${state.testoDaRicercare}`)
        .then((value)=>{
            state.testArraySeries=value.data.results
        })
    }
  } */
};
</script>

<style lang="scss">
.main-background {
  background-color: #434343;
}
.mygap {
  row-gap: 2rem;
}
</style>