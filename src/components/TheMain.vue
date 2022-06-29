<template>
  <div class="main-background">
    <div class="row ">
      <h1>Film</h1>
      <div
        v-for="(value, i) in visualizzaArrayStore"
        :key="value + i"
        class="col-3"
      >
        <CardofDFilm :myProps="value"></CardofDFilm>
      </div>
    </div>
    <div class="row ">
      <h1>Serie TV</h1>
      <div
        v-for="(value, i) in visualizzaArrayStoreSerieTV"
        :key="value + i"
        class="col-3"
      >
        <CardofSeries :myProps="value"></CardofSeries>
      </div>
    </div>

    <!--  <ul>
      <h1>Film:</h1>
      <li v-for="(value, i) in visualizzaArrayStore" :key="value + i">
        <h2><strong>Titolo:</strong> {{ value.title }}</h2>
        <h3><strong>Titolo Originale:</strong> {{ value.original_title }}</h3>
        <img
          :src="`http://image.tmdb.org/t/p/w500/${value.poster_path}`"
          onerror="javascript:this.src='img/error.webp'"
          height="500"
          alt=""
        />
        <div v-if="value.original_language">
          <span
            >Lingua:
            <img
              :src="`https://flagcdn.com/16x12/${value.original_language}.png`"
              width="16"
              height="12"
              alt=""
              onerror="javascript:this.src='img/error.webp'"
            />
          </span>
          <span class="ms-3">Vote:</span>
          <span
            v-for="(star, i) in getStars(value.vote_average)"
            :key="star + i"
          >
            <i class="fa-solid fa-star"></i>
          </span>
        </div>
      </li>
    </ul>
    <ul>
      <h1>Serie TV:</h1>
      <li v-for="(value, i) in visualizzaArrayStoreSerieTV" :key="value + i">
        <h2><strong>Titolo:</strong> {{ value.name }}</h2>
        <h3><strong>Titolo Originale:</strong> {{ value.original_name }}</h3>
        <img
          :src="`http://image.tmdb.org/t/p/w500/${value.poster_path}`"
          onerror="javascript:this.src='img/error.webp'"
          height="500"
          alt=""
        />
        <div v-if="value.original_language">
          <span
            >Lingua:
            <img
              :src="`https://flagcdn.com/16x12/${value.original_language}.png`"
              width="16"
              height="12"
              alt=""
              onerror="javascript:this.src='img/error.webp'"
            />
          </span>
          <span class="ms-3">Vote:</span>
          <span
            v-for="(star, i) in getStars(value.vote_average)"
            :key="star + i"
          >
            <i class="fa-solid fa-star"></i>
          </span>
        </div>
      </li>
    </ul> -->
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
    getStars(value) {
      return Math.round(value / 2);
    },
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
</style>