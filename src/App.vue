<script setup>
import { ref } from 'vue'

const count = ref(0)

const increment = () => {
  count.value++
}

const decrement = () => {
  count.value--
}

const resetCount = () => {
  count.value = 0
}

const setCountOnEnter = (event) => {
  count.value = parseInt(event.target.value) || 0
}
</script>

<template>
  <div>
    <p 
      :class="{ 'text-red': count >= 10, 'text-green': count === 0 }"
      :style="{ fontSize: count + 16 + 'px' }"
    >
      Nilai count: {{ count }}
    </p>

  
    <p v-if="count === 0">Count masih nol.</p>
    <p v-else-if="count > 0 && count < 10">Count dalam batas normal.</p>
    <p v-else>Count sudah terlalu tinggi!</p>


    <p v-if="count >= 10" class="warning">Batas maksimum tercapai!</p>

    <p>Apakah count genap? {{ count % 2 === 0 ? 'Ya' : 'Tidak' }}</p>
    <p>Perkalian count dengan 2: {{ count * 2 }}</p>


    <input type="number" v-model="count" @keydown.enter="setCountOnEnter" />

    <button @click="increment" :disabled="count >= 10">Tambah</button>

 
    <button v-if="count > 0" @click="decrement">Kurang</button>

    <button @dblclick="resetCount">Reset (Double Click)</button>
  </div>
</template>

<style>
.text-red {
  color: red;
}
.text-green {
  color: green;
}
.warning {
  color: orange;
  font-weight: bold;
}
</style>