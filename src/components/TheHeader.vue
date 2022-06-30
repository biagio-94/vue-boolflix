<template>
  <nav class="py-3 px-3 background">
    <div class="d-flex align-items-center justify-content-between">
      <div class="my-logo">
        <img
          src="https://image.tmdb.org/t/p/original/wwemzKWzjKYJFfCeiB57q3r4Bcm.svg"
          alt=""
        />
      </div>
      <div class="search-bar">
        <input type="text" @change="uploadmyStore()" v-model="testoInserito" />
        <h6 class="text-white">press enter</h6>
      </div>
    </div>
  </nav>
</template>

<script>
import axios from "axios";
import { state } from "../store";
export default {
  data() {
    return {
      userEmail: "",
      userPassword: "",
      testoInserito: "",

      displayLogIn: true,
      databaseUsers: [],
    };
  },
  mounthed: {},

  methods: {
    uploadmyStore() {
      state.userlog = false;
      if (this.testoInserito.length >= 0) {
        state.testoDaRicercare = this.testoInserito;
      }
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
    changeInterface() {
      this.displayLogIn = false;
    },
    checkOnDatabase() {
      axios.get("users.json").then((resp) => {
        console.log(resp.data.users);
        resp.data.users = this.databaseUsers;
        console.log(this.databaseUsers);
      });

      this.databaseUsers.forEach((value) => {
        console.log(value);
        if (
          this.userEmail == value.user_email &&
          this.userPassword == value.user_password
        ) {
          console.log("cao");
        }
      });
    },
  },
};
</script>

<style lang="scss">
.background {
  background-color: black;
}
.my-logo {
  width: 300px;
  img {
    width: 100%;
  }
}
</style>