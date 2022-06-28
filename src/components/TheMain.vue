<template>
  <div>
    <ul>
      <li v-for="(value,i) in visualizzaArrayStore" :key="value + i">
      <h1><strong>Titolo:</strong> {{value.title}}</h1>
      <h3><strong>Titolo Originale:</strong> {{value.original_title}}</h3>
      <span>Lingua:{{value.original_language}} Voto:{{value.vote_average}}</span>

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