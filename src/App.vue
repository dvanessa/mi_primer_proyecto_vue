<script setup>
import {ref, computed} from 'vue'

const name = "Juan";
const styleColor = "color:blue";
const arrayColores = ["red", "blue", "green"];
const activo = true;
const arrayFrutas = [
    {   
      name: "manzana",
        price: "$1.00",
        description: "Una manzana",
        id:1
    },
    {   
      name: "Pera",
        price: "$2.00",
        description: "Una pera",
        id:2
    },
    {   
      name: "Naranja",
        price: "$1.00",
        description: "Una naranja",
        id:3
    },
  ]
  const arrayFavoritos = ref([])
  const handledClick = () =>{
    console.log("holaclick");
  }
  const counter = ref(0);
  const increment = () =>{
    counter.value++;
  }
  const decrement = () =>{
    counter.value--;
  }
  const reset = () =>{
    counter.value = 0;
  }
  const add = () => {
    arrayFavoritos.value.push(counter.value);
  }
  const classCounter = computed(() => {
    if(counter.value === 0)
      return 'zero';
      else if(counter.value > 0)
      return 'positive';
      else if(counter.value < 0)
      return 'negative';
  })
  const bloquearBtnAdd = computed(() => {
    const numSearch = arrayFavoritos.value.find((num) => num === counter.value);
    return numSearch || numSearch === 0
  });

</script>
<template>
  <div class="content-fluid">
  <h1>Hola {{ name }}</h1>
  <br/>
  <p><h2 :style="`color:${arrayColores[2]}`">soy orange</h2></p>
  <br/>
  <p><h2>{{ arrayColores }}</h2></p>
  <br/>
  <h2 v-if="!activo">Es inactivo</h2>
  <h2 v-else>Es activo</h2>
<ul>
  <li 
  v-for="(frutas, index) in arrayFrutas" v-bind:key="frutas.id"
  >
  {{index + 1}} {{ frutas.name }} {{ frutas.description }} {{ frutas.price }}
  </li>
</ul>
<h2 :class="classCounter">{{ counter }}</h2>
<button v-on:click="increment()" class="btn btn-success">incrementar</button>
<button v-on:click="decrement()" class="btn btn-warning">decrementar</button>
<button v-on:click="reset()" class="btn btn-danger">reset</button>
<button @click="add" :disabled="bloquearBtnAdd" class="btn btn-secondary">Add</button>
<br/>
{{ arrayFavoritos }}
<ul>
  <li v-for="item in arrayFavoritos" :key="index">
{{ item }}
  </li>
</ul>
</div>
</template>
<style>
h1 {
  color: red;
}
.positive{
  color:green;
}
.negative{
  color:red;
}
.zero{
  color:peru;
}
</style>
