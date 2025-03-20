<template>
  <div>
    <h2>History Perubahan count</h2>
    <ul>
      <li v-for="(change, index) in history" :key="index">
        {{ change }}
      </li>
    </ul>

    <h2>Informasi Count</h2>
    <p>Count saat ini: {{ count }}</p>
    <p>Status Count: {{ countStatus }}</p>

    <p v-if="countChangeMessage">{{ countChangeMessage}}</p>

    <h2>Input Count</h2>
    <input
      type="number"
      v-model="count"
      @keydown.enter="setCountOnEnter"
      ref="count Input"
    />

    
    <button @click="increment" :disabled="count >= 10">Tambah</button>
    <button v-if="count > 0" @click="decrement">Kurang</button>
    <button @dblclick="resetCount">Reset (Double Click)</button>

    <p v-if="count === 0">Count masih nol.</p>
    <p v-else-if="count > 0 && count < 10">Count dalam batas normal.</p>
    <p v-else>Count sudah terlalu tinggi!</p>


    <p v-if="count >= 10" class="warning">Batas maksimum tercapai!</p>

    <p>Apakah count genap? {{ count % 2 === 0 ? 'Ya' : 'Tidak' }}</p>
    <p>Perkalian count dengan 2: {{ count * 2 }}</p>
  </div>
</template>
<script setup>
import { ref, computed, watch, onMounted } from 'vue'

const count = ref(0);
const history = ref([]);
const countChangeMessage = ref('');
const countInput = ref(null);
const countStatus = computed(() => {
  if (count.value === 0) return 'Count masih nol. ';
  if (count.value > 0 && count.value < 10) return 'Count dalam batas normal';
  return 'Count sudah terlalu tinggi!';
});

const isEven = computed(() => count.value % 2 === 0);
const doubledCount = computed(() => count.value * 2);

watch(count, (newValue, oldValue) => {
  countChangeMessage.value = `Count berubah dari ${oldValue} menjadi ${newValue}`;
  history.value.push(`Count berubah: ${oldValue} -> ${newValue}`);
});

onMounted(() => {
  countInput.value.focus();
});

const increment = () => {
  if(count.value < 10) {
    count.value++;
  }
};

const decrement = () => {
  if(count.value > 0) {
    count.value--;
  }
}

const resetCount = () => {
  count.value = 0;
};

const setCountOnEnter = (event) => {
  count.value = parseInt(event.target.value) || 0;
};
</script>

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