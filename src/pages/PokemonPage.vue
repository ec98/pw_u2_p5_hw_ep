<template>
  <div v-show="gameMenu">
    <h1 v-if="!ganadorId">Espere por favor... loading...</h1>
    <div class="assertPokemon" v-else>
      <h1>Adivina el pokemon</h1>
      <div class="acumuladores">
        <h2>Puntaje: {{ puntaje }}</h2>
        <h2>Intento: {{ intento }}</h2>
      </div>
      <PokemonImagen :pokemonId="ganadorId.id" :showPokemon="viewPokemon" />
      <PokemonOpciones @comunicate="viewOnClickOptions($event)" :listaPokemons="arrPokemons" />
    </div>
  </div>
  <div class="winnerPlayer" v-if="winnerPlayer">
    <h2>Felicidades, has capturado a tu pokemon {{ namePokemon }}.</h2>
    <PokemonImagen :pokemonId="ganadorId.id" :showPokemon="viewPokemon" />
    <div class="winnerPlayer-reiniciar">
      <button @click="reiniciar()">Reiniciar Juego</button>
    </div>
  </div>
  <div class="loserPlayer" v-if="lostPlayer">
    <h2>Perdiste por {{ intento }} intentos.</h2>
  </div>
  <div class="loserPlayer-reiniciar" v-if="lostPlayer">
    <button @click="reiniciar()">Reiniciar Juego</button>
  </div>
</template>
  
<script>
import PokemonImagen from "../components/PokemonImagen.vue";
import PokemonOpciones from "../components/PokemonOpciones.vue";

import getPokemonsFachada from "../helpers/PokemonHelper";

export default {
  components: {
    PokemonImagen,
    PokemonOpciones
  },
  beforeCreate() {
    console.log("Antes de que se cree el componente.");
  },
  created() {
    console.log("Se creo el componente.");
  },
  beforeMount() {
    console.log("Antes de que mounte carge el componenten en la pagina.");
  },
  mounted() {
    console.log("se monto el componente pokemon page.");
    this.construirLoad();
  },
  beforeUpdate() {
    console.log("Antes de que se actualice el componente.");
  },
  updated() {
    console.log("Basicamente, se actualiza el componente.");
  },
  beforeDestroy() {
    console.log("Antes de que se destruya.");
  },
  destroyed() {
    console.log("Destruir");
  },
  methods: {
    async construirLoad() {
      const arrayPokemons = await getPokemonsFachada();
      console.log("Usando el componente de arreglos -> " + arrayPokemons);
      this.arrPokemons = arrayPokemons;
      const indexWinner = Math.floor(Math.random() * 4);
      this.ganadorId = this.arrPokemons[indexWinner];
    },
    viewOnClickOptions(dataOption) {
      this.intento++;
      console.log("Dio click y enviando reporte.", dataOption);
      //desestructurando...
      console.log("Id pokemon -> ", dataOption.id);
      console.log("Nombre pokemon -> ", dataOption.name);
      console.log("Hobby -> ", dataOption.hobby);
      if (dataOption.id === this.ganadorId.id) {
        this.viewPokemon = true;
        this.puntaje += 5;
        // console.log("ganaste");
        this.gameMenu = false;
        this.winnerPlayer = true;
        this.lostPlayer = false;
        this.namePokemon = dataOption.name;
      }
      if (this.intento >= 2) {
        this.lostPlayer = true;
        this.winnerPlayer = false;
        this.gameMenu = false;
      }
    },
    reiniciar() {
      this.construirLoad();
      this.gameMenu = true;
      this.arrPokemons = [];
      this.ganadorId = null;
      this.namePokemon = null;
      this.viewPokemon = false;
      this.winnerPlayer = false;
      this.lostPlayer = false;
      this.puntaje = 0;
      this.intento = 0;
    }
  },
  data() {
    return {
      mostrarVentana: true,
      gameMenu: true,
      arrPokemons: [],
      ganadorId: null,
      namePokemon: null,
      viewPokemon: false,
      winnerPlayer: false,
      lostPlayer: false,
      puntaje: 0,
      intento: 0
    };
  }
};
</script>
  
<style>
h1 {
  text-align: center;
}

.assertPokemon {
  text-align: center;
  color: rgb(60, 0, 255);
  font-family: "Times New Roman", Times, serif;
}

.acumuladores {
  color: black;
  display: grid;
  margin: 20px;
  grid-template-columns: repeat(2, 200px);
  justify-content: center;
  align-items: center;
}
.winnerPlayer {
  display: grid;
  grid-template-rows: repeat(1, 200px);
  justify-content: center;
  align-items: center;
  font-size: 30px;
  color: rgb(127, 127, 218);
}
h3 {
  text-align: center;
  color: rgb(187, 93, 176);
}
.loserPlayer {
  display: flex;
  font-size: 30px;
  justify-content: center;
  align-items: center;
  color: rgb(233, 149, 149);
}
.winnerPlayer-reiniciar {
  display: flex;
  justify-content: center;
  align-items: center;
  margin: 20px;
}
button {
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  text-align: center;
  font-size: 20px;
  cursor: pointer;
  border-radius: 4px;
  color: black;
}

button:hover {
  background: aqua;
}
.loserPlayer-reiniciar {
  display: flex;
  justify-content: center;
  align-items: center;
}
</style>