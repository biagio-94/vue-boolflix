<template>
  <div class="backgronud">
    <nav class="d-flex justify-content-between py-3 px-3 align-items-center">
      <div class="logo-container">
        <img
          src="https://image.tmdb.org/t/p/original/wwemzKWzjKYJFfCeiB57q3r4Bcm.svg"
          alt=""
        />
      </div>
      <a class="btn my-button px-5" @click="changeInterface()"
        ><strong class="text-white">Accedi</strong></a
      >
    </nav>

    <div class="container centrate" :class="{ 'd-none': !displayLogIn }">
      <h1>Film, serie TV e tanto altro. Senza limiti.</h1>
      <h4>Guarda ciò che vuoi ovunque. Disdici quando vuoi.</h4>
      <h6 class="mt-2">
        Vuoi guardare Netflix? Inserisci l'indirizzo email per abbonarti o
        riattivare il tuo abbonamento.
      </h6>
      <div class="d-flex pt-2">
        <input style="width: 400px" type="text" placeholder="Indirizzo email" />
        <button class="btn my-button px-3">
          <strong class="text-white">INIZIA ></strong>
        </button>
      </div>
    </div>
    <div class="container centrate">
      <div class="accesso" :class="{ 'd-none': displayLogIn }">
        <h2>Accedi</h2>
        <div class="form-floating mb-3">
          <input
            v-model="userEmail"
            type="email"
            class="form-control"
            id="floatingInput"
            placeholder="Indirizzo email"
          />
          <label for="floatingInput">Email address</label>
        </div>
        <div class="form-floating">
          <input
            v-model="userPassword"
            type="password"
            class="form-control"
            id="floatingPassword"
            placeholder="Password"
          />
          <label for="floatingPassword">Password</label>
          <a class="btn my-button px-5 mt-3 w-100" @click="checkOnDatabase()"
            ><strong class="text-white">Accedi</strong></a
          >
        </div>
        <div class="d-flex justify-content-between mt-2">
          <span> <input type="checkbox" /> Ricordami </span>
          <span><a href="">Ti serve auto?</a></span>
        </div>
        <div class="mt-5">
          <h6>Prima volta su Netflix? <a href="">Registrati</a></h6>
          <span class="my-txt"
            >Questa pagina è protetta da Google reCAPTCHA per garantire che tu
            non sia un bot. <a href="">Scopri di più.</a></span
          >
        </div>
      </div>
    </div>
  </div>
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
      databaseUsers:[]
    };
  },
  mounthed: {
    
  },

  methods: {
    uploadmyStore() {
      state.userlog = false;
      if (this.testoInserito.length >= 0) {
        state.testoDaRicercare = this.testoInserito;
      }
    },
    changeInterface() {
      this.displayLogIn = false;
    },
    checkOnDatabase(){
      axios.get("users.json").then((resp) => {
        console.log(resp.data.users);
        resp.data.users=this.databaseUsers
        console.log(this.databaseUsers);
      });
      
      
      this.databaseUsers.forEach(value=>{
        console.log(value);
        if(this.userEmail==value.user_email && this.userPassword==value.user_password){console.log("cao");}
      })
      
    }
  },
};
</script>

<style lang="scss">
.backgronud {
  background-image: url("../assets/IT-it-20220620-popsignuptwoweeks-perspective_alpha_website_large.jpg");
  background-size: cover;
  background-position: center;
  height: 100%;
  .logo-container {
    width: 200px;
    img {
      width: 100%;
    }
  }
  .my-button {
    background-color: #e50914;
    &:hover {
      background-color: #e50914;
    }
  }
  .centrate {
    height: 90%;
    color: white;
    display: flex;
    flex-direction: column;
    flex-grow: 1;
    justify-content: center;
    align-items: center;
  }
  .accesso {
    background-color: rgba($color: #000000, $alpha: 0.5);
    width: 400px;
    padding: 2rem 1rem;
    color: #000000;
    .my-txt {
      font-size: 0.8rem;
      color: white;
    }
    h2,
    h6,
    span {
      color: white;
    }
  }
}
</style>