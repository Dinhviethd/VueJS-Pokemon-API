<template>
  <div>
    <h1 class="header">Pokemon API</h1>
    <div class="SearchBar">
      <input
        v-model="searchQuery"
        type="text"
        placeholder="Search some Pokemon"
      />
    </div>
    <div class="content">
      <p v-if="loading" style="text-align:center;">Getting Data From Pokedeck...</p>
      <p v-else-if="filteredPokemon.length === 0" style="text-align: center; font-size: 20px;">
        No Pokémon found 😢
      </p>
      <div
        v-else
        class="Pokemon"
        v-for="pokemon in filteredPokemon"
        :key="pokemon.id"
      >
        <span style="margin-left: 40%">#{{ pokemon.id }} <br /></span>
        <img class="photo" :src="pokemon.img" :alt="pokemon.name" />
        <h3>{{ pokemon.name }}</h3>
        <div class="Element">
          <span
            v-for="type in pokemon.types"
            :key="type"
            :class="['Type', type]"
          >
            {{ type }}
          </span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, computed, onMounted } from "vue";

const searchQuery = ref("");
const allPokemon = ref([]);
const loading = ref(false);

// Fetch danh sách Pokémon
async function loadPokemon() {
  loading.value = true;
  try {
    const response = await fetch("https://pokeapi.co/api/v2/pokemon");
    const firstAPI = await response.json();
    const arr = firstAPI.results;

    allPokemon.value = [];

    for (let i = 0; i < arr.length; i++) {
      const response2 = await fetch(arr[i].url);
      const info = await response2.json();
      allPokemon.value.push({
        id: info.id,
        name: info.name.toLowerCase(),
        img: info.sprites.other.home.front_default,
        types: info.types.map((t) => t.type.name),
      });
    }
  } catch (error) {
    console.error("Error fetching Pokémon data:", error);
  } finally {
    loading.value = false;
  }
}

const filteredPokemon = computed(() => {
  const query = searchQuery.value.toLowerCase();
  return allPokemon.value.filter((pokemon) =>
    pokemon.name.includes(query)
  );
});

onMounted(() => {
  loadPokemon();
});
</script>

<style>
* {
  font-family: Arial;
}
body{
  background-color: white;
}

.header {
  font-size: 40px;
  text-align: center;
  color: rgb(4, 4, 80);
  font-weight: lighter;
}

input {
  border-radius: 30px;
  padding: 15px;
  width: 400px;
  margin: 30px 0;
  box-shadow: 0 2px 8px var(--black);
  border: 1px solid var(--black);
}

.SearchBar {
  text-align: center;
}

.Pokemon {
  border-radius: 20px;
  background-color: rgb(255, 255, 255);
  padding: 30px;
  box-shadow: 0 2px 8px var(--black);
  width: 200px;
  margin-bottom: 30px;
}

.Pokemon img {
  position: relative;
  left: 10px;
  width: 200px;
  height: auto;
}

.Pokemon h3 {
  text-align: center;
  margin-bottom: 5px;
  font-weight: bolder;
  color: rgb(5, 5, 104);
}

.Pokemon span {
  color: rgb(5, 5, 104);
  font-size: larger;
  font-weight: bold;
}

.content p {
  font-size: 30px;
  color: gray;
}

.Type {
  padding: 5px;
  border-radius: 5px;
}

.Element {
  display: flex;
  justify-content: center;
  gap: 5px;
  font-weight: bold;
}

.grass {
  background-color: rgb(11, 155, 11);
}

.fire {
  background-color: rgb(233, 14, 14);
}

.poison {
  background-color: rgb(145, 6, 145);
}

.flying {
  background-color: gray;
}

.bug {
  background-color: rgb(14, 236, 21);
}

.normal {
  background-color: rgb(210, 209, 209);
}

.water {
  background-color: rgb(16, 161, 218);
}

.photo {
  padding-top: 20px;
  height: 100px;
}

.content {
  display: flex;
  justify-content: center;
  gap: 50px;
  flex-wrap: wrap;
}

:root {
  --black: rgba(0, 0, 0, 0.2);
}
</style>