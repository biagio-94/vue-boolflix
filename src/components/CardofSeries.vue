<template>
    <div class="card">
        
        <img
          :src="`http://image.tmdb.org/t/p/w500/${myProps.poster_path}`"
          onerror="javascript:this.src='img/error.webp'"
          height="500"
          alt=""
        />
    </div>
</template>
<script>
export default {
    props:{
        myProps: Object
    }
}
</script>
<style lang="scss">
    
</style>