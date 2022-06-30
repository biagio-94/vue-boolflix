<template>
<div class="getrelative onHoverHidden">
  <div class="card ">
    <img class=""
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
    </div>
  </div>
</template>
<script>
export default {
  props: {
    myProps: Object,
  },
  methods: {
    getStars(value) {
      return Math.round(value / 2);
    },
  },
};
</script>
<style lang="scss">
i {
  color: yellow;
}
.getrelative{
  position: relative;
  
}
.my-card {
  position: absolute;
 
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  transition: .5s ease;
  opacity: 0;
  background-color: black;
  color: white;
  display: block;
  height: 500px;
  overflow: auto;
  padding: 1rem 1rem;
}
.onHoverHidden{
  
  &:hover .my-card{
  opacity: 1;
 
 }
 
}

</style>