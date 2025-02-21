<!-- <script setup>
import { ref, computed } from 'vue'

const listPokemon = ref([
  {
    name: 'Pikachua',
    type: 'Electric'
  },
  {
    name: 'Charmander',
    type: 'Fire',
    color: 'Yellow'
  },
  {
    name: 'Squirtle',
    type: 'Water'
  },
  {
    name: 'Jigglypuff',
    type: 'Normal'
  },
  {
    name: 'Meowth',
    type: 'Normal'
  },
  {
    name: 'Psyduck',
    type: 'Water'
  },
  {
    name: 'Bulbasaur',
    type: 'Grass'
  }
])
const valueInput = ref('')
const textareaValue = ref('')
const filterdPokemon = computed(function() {
 
 const filterByName = listPokemon.value.filter(function(item) {
    return item.name.toLowerCase().includes(valueInput.value.toLowerCase().trim())
  })

  return filterByName.map(item => {
    return {
      ...item,
      name:item.name.toUpperCase(),
      age: 10
    }
  })
})
</script>

<template>
  <div>
    <label for="111">Giá trị: {{ valueInput }}</label>
    <br>
    <input type="text" id="111" placeholder="Search..."
      v-model="valueInput"
    >
    <br>
    <ul>
      <span>
        Total: {{ filterdPokemon.length }}
      </span>
    <li v-for="(pokemon,index) in filterdPokemon" :key="index">
      {{ pokemon.name }} - {{ pokemon.type }}: {{ pokemon.age }}
    </li>
    </ul>
  </div>
</template>
<style>

</style> -->
<script  setup>
  import {ref } from 'vue'
  let pokemon= ref([])
</script>
<template>
  <h1 class="header">Pokemon API</h1>
    <div class="SearchBar"><input type="text" placeholder="Search some Pokemon"></div>
    <div class="content"></div>
</template>
<style>
*{
    font-family: Arial;
}
.header{
    font-size: 40px;
    text-align: center;
    color: rgb(4, 4, 80);
    font-weight: lighter;
}
input{
    border-radius: 30px;
    padding: 15px;
    width: 400px;
    margin: 30px 0;
    box-shadow: 0 2px 8px var(--black);
    border: 1px solid var(--black);
}
.SearchBar{
    text-align: center;
}
.Pokemon{
    border-radius: 20px;
    background-color: rgb(255, 255, 255);
    padding: 30px;
    box-shadow: 0 2px 8px var(--black);
    width: 200px;
    margin-bottom: 30px;
}
.Pokemon img{
    position:relative;
    left: 10px;
    width: 200px;
    height: auto;
}
.Pokemon h3{
    text-align: center;
    margin-bottom: 5px;
}
.Pokemon span{
    color: rgb(4, 4, 80);
    font-size: larger;
}
.content p{
    font-size: 30px;
    color: gray;
}
.Type{
    padding: 5px;
    border-radius: 5px;
    
}
.Element{
    display: flex;
    justify-content: center;
    gap: 5px;
    font-weight: bold;
}
.grass{
    background-color: rgb(11, 155, 11);
}
.fire{
    background-color: rgb(233, 14, 14);
}
.poison{
    background-color: rgb(145, 6, 145);
}
.flying{
    background-color: gray;
}
.bug{
    background-color: rgb(14, 236, 21);;
}
.normal{
    background-color: rgb(210, 209, 209);
}
.water{
    background-color: rgb(16, 161, 218);
}
.photo{
    padding-top: 20px;
    height: 100px;
}
.content{
    display: flex;
    justify-content: center;
    gap: 50px;
    flex-wrap: wrap; 
}

:root{
    --black: rgba(0, 0, 0, 0.2); 
}
</style>
