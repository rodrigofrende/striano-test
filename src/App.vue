<template>
  <main class="">
    <div class="d-flex pt-3" v-if="pokemon">
      <h1 class="mx-auto text-capitalize">{{ pokemon.name }}</h1>
    </div>
    <div class="home d-flex justify-content-center py-3">
      <img
        v-if="pokemon"
        :src="pokemon.sprites.front_default"
        class="img-fluid"
      />
    </div>
    <div class="d-flex">
      <button
        type="button"
        @click="getAnotherPokemon"
        class="btn btn-primary mx-auto"
      >
        Get Another!
      </button>
    </div>
  </main>
</template>

<script setup>
import { ref, onMounted } from "vue";

const pokemon = ref(null);

const getAnotherPokemon = () => {
  const id = Math.floor(Math.random() * 151) + 1;
  fetch(`https://pokeapi.co/api/v2/pokemon/${id}`)
    .then((response) => response.json())
    .then((data) => (pokemon.value = data));
};

onMounted(() => {
  getAnotherPokemon();
});
</script>

<style>
@import "./assets/base.css";

#app {
  margin: 0 auto;
  padding: 0;
  font-weight: normal;
  height: 100vh;
}
.img-fluid {
  min-height: 200px;
  border-radius: 50%;
  padding: 2px;
}

@media (hover: hover) {
  a:hover,
  .btn:hover {
    background-color: hsla(221, 94%, 50%, 0.2);
  }
}
</style>
