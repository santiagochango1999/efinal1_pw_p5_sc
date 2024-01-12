<template>
  <div class="valor">
    <h1>Puntaje:{{ puntaje }}</h1>
    <h1>Intento:{{ intento }}</h1>
  </div>
  <div class="compo1">
    <Juego :url="url1" :nom="nom1" />
    <Juego :url="url2" :nom="nom2" />
    <Juego :url="url3" :nom="nom3" />
  </div>
  <button v-on:click="consumirApi()">JUGAR</button>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'
import Juego from "./components/Juego.vue";
export default {
  name: "App",
  components: {
    Juego,
  },
  data() {
    return {
      url1: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/3.svg",
      url2: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/2.svg",
      url3: "https://raw.githubusercontent.com/PokeAPI/sprites/master/sprites/pokemon/other/dream-world/1.svg",
      nom1: "xxxxxxxxx",
      nom2: "xxxxxxxxx",
      nom3: "xxxxxxxxx",
      puntaje: 0,
      intento: 0,
      consumir: [],
      p: true,
    };
  },
  methods: {
    async consumirApi() {
      for (let index = 0; index < 3; index++) {
        const { answer, image } = await fetch("https://yesno.wtf/api").then(
          (r) => r.json()
        );
        this.consumir.push({ answer, image });
      }
      if (this.p === true) {
        const { answer, image } = this.consumir[0];
        this.url1 = image;
        this.nom1 = answer;
      }
      if (this.p) {
        const { answer, image } = this.consumir[1];
        this.url2 = image;
        this.nom2 = answer;
      }
      if (this.p) {
        const { answer, image } = this.consumir[2];
        this.url3 = image;
        this.nom3 = answer;
      }

      if (this.nom1 === this.nom2 === this.nom3) {
        this.puntaje = this.puntaje + 5;
        return this.puntaje;
      } else if (
        this.nom1 === this.nom2 ||
        this.nom1 === this.nom3 ||
        this.nom2 === this.nom3
      ) {
        this.puntaje = this.puntaje + 2;
        return this.puntaje;
      }
      for (let index = 0; index < 3; index++) {
        this.consumir.pop();
      }
    }
    
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
.compo1,
.valor {
  display: grid;
  justify-content: center;
  align-items: center;
  padding: 15px 15px;
}
.compo1 {
  grid-template-columns: repeat(3, 500px);
}
.valor {
  grid-template-columns: repeat(2, 500px);
}
button {
  height: 200Ppx;
  width: 130px;
  font-size: 30px;
  font-family: "Franklin Gothic Medium", "Arial Narrow", Arial, sans-serif;
}
</style>
