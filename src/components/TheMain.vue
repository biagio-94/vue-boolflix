<template>
  <div>
    <ul>
      <li v-for="(value, i) in visualizzaArrayStore" :key="value + i">
        <h1><strong>Titolo:</strong> {{ value.title }}</h1>
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
  },
};
</script>

<style lang="scss">
</style>