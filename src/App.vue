<template>
  <div id="app">
    <TheHeader v-if="headerVisualiza"></TheHeader>
    <TheMain v-else></TheMain>
  </div>
</template>

<script>
import TheHeader from './components/TheHeader.vue';
import TheMain from './components/TheMain.vue'
import { state } from "./store";
export default {
  data() {
    return {
      
    }
  },
  computed:{
    headerVisualiza(){
      return state.userlog
    }
  },
  name: 'App',
  components: {
    TheHeader,TheMain
  }
}
</script>

<style lang="scss">
@import "../node_modules/bootstrap/scss/bootstrap.scss";
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  height: 100vh;
  
}
</style>
