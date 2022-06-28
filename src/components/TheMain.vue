<template>
  <div>
    <ul>
        <h1>Film:</h1>
      <li v-for="(value, i) in visualizzaArrayStore" :key="value + i">
        <h2><strong>Titolo:</strong> {{ value.title }}</h2>
        <h3><strong>Titolo Originale:</strong> {{ value.original_title }}</h3>
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
            Voto:{{ value.vote_average }}</span
          >
        </div>
      </li>
        <h1 class="py-5">Serie TV:</h1>
      <li v-for="(value, i) in visualizzaArrayStoreSerieTV" :key="value + i">
        <h2><strong>Titolo:</strong> {{ value.name }}</h2>
        <h3><strong>Titolo Originale:</strong> {{ value.original_name }}</h3>
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
            Voto:{{ value.vote_average }}</span
          >
        </div>
      </li>
    </ul>
  </div>
</template>

<script>
import { state } from "../store";
export default {
  computed: {
    visualizzaArrayStore() {
      return state.testArray;
    },
    visualizzaArrayStoreSerieTV() {
      return state.testArraySeries;
    },
  },
};
</script>

<style lang="scss">
</style>