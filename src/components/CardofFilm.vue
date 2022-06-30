<template>
  <div class="getrelative onHoverHidden" @mouseenter="takeActor(myProps.id)">
    <div class="card">
      <img
        class=""
        :src="`http://image.tmdb.org/t/p/w500/${myProps.poster_path}`"
        onerror="javascript:this.src='img/error.webp'"
        height="500"
        alt=""
      />
    </div>
    <div class="my-card">
      <p><strong>Titolo:</strong> {{ myProps.title }}</p>
      <p><strong>Titolo Originale:</strong> {{ myProps.original_title }}</p>
      <p style="display: inline" class=""><strong>Vote:</strong></p>
      <span v-for="(star, i) in 5" :key="star + i">
        <i
          v-if="i < getStars(myProps.vote_average)"
          class="fa-solid fa-star"
        ></i>
        <i v-else class="fa-regular fa-star"></i>
      </span>
      <p class="mt-2"><strong>Overview: </strong>: {{ myProps.overview }}</p>
      <h6>Actor:</h6>
      <p class="mt-2">
        <strong v-for="(name, i) in actorNames" :key="name.id + `ciao`"
          ><span v-if="i < actorNames.length - 1">{{ name.name }}, </span>
          <span v-else>{{ name.name }}</span></strong
        >
      </p>
      <h6>Generi:</h6>
      <p class="mt-2">
        <strong v-for="(name, i) in generi" :key="i + `ciao`"
          ><span v-if="i < generi.length - 1">{{ name.name }}, </span>
          <span v-else>{{ name.name }}</span></strong
        >
      </p>
    </div>
  </div>
</template>
<script>
import axios from "axios";
export default {
  props: {
    myProps: Object,
  },
  data() {
    return {
      actorNames: [],
      generi: [],
    };
  },
  methods: {
    getStars(value) {
      return Math.round(value / 2);
    },
    takeActor(callID) {
      axios
        .get(
          `https://api.themoviedb.org/3/movie/${callID}/credits?api_key=c47fc9efae23d89f94e602631b3ba67e`
        )
        .then((resp) => {
          let actors = resp.data.cast;
          for (let i = 0; i < 5; i++) {
            this.actorNames.push(actors[i]);
          }
        });
      axios
        .get(
          `https://api.themoviedb.org/3/movie/${callID}?api_key=c47fc9efae23d89f94e602631b3ba67e`
        )
        .then((resp) => {
          console.log(resp.data.genres);
          this.generi = resp.data.genres;
        });
    },
  },
};
</script>
<style lang="scss">
i {
  color: yellow;
}
.getrelative {
  position: relative;
}
.my-card {
  position: absolute;

  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  transition: 0.5s ease;
  opacity: 0;
  background-color: black;
  color: white;
  display: block;
  height: 500px;
  overflow: auto;
  padding: 1rem 1rem;
}
.onHoverHidden {
  &:hover .my-card {
    opacity: 1;
  }
}
</style>