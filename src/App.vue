<script setup>
// import  HelloWorld  from "./components/HelloWorld.vue"
import { onMounted, ref } from "vue";

const newItem = ref(0);

const dataset = [300, 50, 100];

let chart = null;

const data = {
  labels: ["Red", "Blue", "Yellow"],
  datasets: [
    {
      label: "My First Dataset",
      data: dataset,
      backgroundColor: [
        "rgb(255, 99, 132)",
        "rgb(54, 162, 235)",
        "rgb(255, 205, 86)",
      ],
      hoverOffset: 4,
    },
  ],
};

const config = {
  type: "pie",
  data: data,
};

const updateChart = () => {
  dataset.push(newItem.value)
  chart.data.datasets[0].data = dataset
  chart.update()
}

onMounted(() => {
  const ctx = document.getElementById("chart");
  chart = new Chart(ctx, config);
});


</script>

<template>
  <div class="mx-auto w-[600px] h-[600px] bg-gray-400">
    <canvas id="chart"> </canvas>
  </div>

  <div class="mt-10">
    <input type="text" v-model="newItem" />
    <button
      @click="updateChart"
      class="ml-2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded mb-10"
    >
      Add More
    </button>
  </div>

  <!-- <HelloWorld /> -->
</template>


<style scoped></style>
