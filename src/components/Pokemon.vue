<template>
  <div class="container">
    <div class="generalPokemon">
      <div class="pokemonID">
        <h2>Pokemon</h2>
        <label for>ID </label>
        <input @input="updatePokemon" @keypress.enter="pressEnter" v-model="id" />
      </div>
      <div>
        <img v-show="mostrar" v-bind:src="img" alt />
      </div>
      <div class="form">
        <label for="idNombre">Nombre</label>
        <input v-show="mostrar" v-model="nombre" id="idNombre" type="text" />

        <label for="idAncho">Ancho</label>
        <input v-show="mostrar" v-model="ancho" id="idAncho" type="text" />

        <label for="idExperiencia">Experiencia</label>
        <input v-show="mostrar" v-model="experiencia" id="idExperiencia" type="text" />
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      id: null,
      nombre: "",
      ancho: "",
      experiencia: "",
      mostrar: true,
      img: null
    };
  },
  methods: {
    async getAPIPokemon() {
      const pokemon = await fetch(
        "https://pokeapi.co/api/v2/pokemon/" + this.id
      ).then(p => p.json());
      this.nombre = pokemon.name;
      this.ancho = pokemon.weight;
      this.experiencia = pokemon.base_experience;
      const animation = pokemon.sprites.back_default;
      this.img = animation;
    },
    pressEnter(e) {
      if (e.keyCode === 13) {
        this.mostrar = true;
        this.getAPIPokemon();
      }
    },
    updatePokemon() {
      this.nombre = "";
      this.ancho = "";
      this.experiencia = "";
      this.img = null;
    }
  },
  watch: {
    id() {
      this.updatePokemon();
    }
  }
};
</script>

<style scoped>
.container {
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
}

.pokemonID {
  font-family: 'Times New Roman', Times, serif;
  margin-bottom: 20px;
}

.form {
  display: grid;
  font-family: "Segoe UI", Tahoma, Geneva, Verdana, sans-serif;
  text-align: left;
  gap: 15px;
  padding: 20px;
  width: 270px;
  margin: 50px;
  border-radius: 8px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
  background-color: #fadfbe;
}

.form input {
  padding: 10px;
  border: 1px solid #f89e9e;
  border-radius: 4px;
}

.generalPokemon {
  display: grid;
  width: 420px;
  border-radius: 10px;
  padding: 20px;
  box-shadow: 0 0 20px rgba(0, 0, 0, 0.1);
  background: rgb(247, 175, 159);
  margin: 20px;
}
</style>

