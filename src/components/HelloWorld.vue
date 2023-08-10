<script setup>
import { onMounted, ref } from 'vue';


const newItems = ref('')
const dataset = [65, 59, 80, 81, 26, 55, 40]

let line = null


const config = {
  type: 'line',
  // data: data,
  options: {
    animations: {
      tension: {
        duration: 1000,
        easing: 'linear',
        from: 1,
        to: 0,
        loop: true
      }
    },
    scales: {
      y: { // defining min and max so hiding the dataset does not change scale range
        min: 0,
        max: 100
      }
    }
  }
};


const data = {
  labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July'],
  datasets: [{
    label: 'Looping tension',
    data: dataset,
    fill: false,
    borderColor: 'rgb(75, 192, 192)',
  }]
};

onMounted(() => {
  const ctx = document.getElementById("line");
  line = new Chart (ctx, config)
})

const addToLine = () => {
  dataset.push(newItems.value)
  line.data.datasets[0].data = dataset
  line.update()
}

</script>

<template>
  <div class="mx-auto w-[600px] h-[600px] bg-gray-400">
    <canvas id="line"> </canvas>
  </div>

  <div class="mt-10">
    <input type="text" v-model="newItems"/>
    <button
      @click="addToLine"
      class="ml-2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded"
    >
      Add More
    </button>
  </div>
</template>

<style scoped>
</style>
