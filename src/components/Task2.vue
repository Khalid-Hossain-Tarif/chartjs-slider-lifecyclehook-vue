<script setup>
import { onBeforeUnmount, onMounted, ref } from 'vue';
// import { Chart, registerables } from 'chart.js'
// Chart.register(...registerables)
import Chart from 'chart.js/auto' //can do it using upper 2 lines


const newItem = ref(50);
let chart = null;
const dataset = [300, 50, 100, 80];

const data = {
  labels: [
    'Red',
    'Blue',
    'Green',
    'Yellow'
  ],
  datasets: [{
    label: 'My First Dataset',
    data: dataset,
    backgroundColor: [
      'rgb(255, 99, 132)',
      'rgb(54, 162, 235)',
      'rgb(54, 162, 15)',
      'rgb(255, 205, 86)',
    ],
    hoverOffset: 4
  }]
};

const config = {
  type: 'pie',
  data: data
};

onMounted(() => {
    const ctx = document.getElementById('myChart');
    chart = new Chart(ctx, config)
});

const updateChart = () => {
    dataset.push(newItem.value);
    chart.data.datasets[0].data = dataset;
    chart.update()
}

onBeforeUnmount(() => {
    if (chart) {
        chart.destroy();
        chart = null;
    }
});
</script>

<template>  
  <div class="mx-auto my-10 w-[400px] h-[400px] bg-gray-300">
    <canvas id="myChart">
    </canvas>
  </div>

  <div class="mt-10 mx-auto w-[400px]">
    <input type="text" name="" id="" v-model="newItem" class="border border-gray-400 px-4 py-2 rounded mr-2">
    <button class="bg-blue-600 text-white font-semibold px-4 py-2 rounded" @click="updateChart()">Add</button>
  </div>
</template>