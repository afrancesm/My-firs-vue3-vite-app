<script setup>

import {ref, computed} from 'vue'

const contador = ref(0);
const favoritos = ref([]);
let isDisabled = true;

const addCount = () => {
  contador.value++;
}
const subsCount = () => {
  contador.value--;
}
const resetAll = () => {
  contador.value = 0;
  favoritos.value = [];
}
const addToFav = () => {
  favoritos.value.push(contador.value)
} 
// Propiedad computada. Devuelve true si Contador existe en Favoritos
const checkDisabled = computed (() => {
  return favoritos.value.includes(contador.value);
})

// Propiedad computada. Devuelve el nombre de una clase dependiendo de si el contador
// es positivo o negativo.
const checkStatus = computed(() => {
  if(contador.value >= 0){
    return "success";
  }else{
    return "warning"
  }
} )

</script>

<template>
<h1>Counter: <span :class="checkStatus">{{ contador }}</span></h1>
<section>
<div class="button-group">
  <button @click="addCount">+</button>
  <button @click="subsCount">-</button>
  <button @click="addToFav" :disabled="checkDisabled">⭐</button>
  <button @click="resetAll">Reset All</button>
</div>
</section>
<section>
<h2>My favorites: </h2>
{{ favoritos }}
</section>
</template>

<style scoped>
.warning{
  color: red;
}
.success{
  color: green;
}
</style>
