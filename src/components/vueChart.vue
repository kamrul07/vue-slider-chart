<script setup >
 import { ref , onMounted , onBeforeUnmount, nextTick } from 'vue'

 const newItem = ref(16);
 const dataset = [1,2,3,4,5,6,7,8,9,10,11,12,13,14,15];
 let chart = null;
 const data = {
  labels: [
    'Red',
    'Blue',
    'Yellow'
  ],
  datasets: [{
    label: 'My First Dataset',
    data: dataset,
    backgroundColor: [
      'rgb(255, 99, 132)',
      'rgb(54, 162, 235)',
      'rgb(255, 205, 86)',
      'rgb(43, 105, 86)',
      'rgb(21, 21, 186)',
    ],
    hoverOffset: 4
  }]
};

const config = {
  type: 'pie',
  data: data,
};

onMounted(() => {
  const ctx = document.getElementById('chart')
  chart = new Chart(ctx, config)
})


function updateChart(){
  dataset.push(newItem.value)
  chart.destroy(); 
  nextTick(() => {
    chart = new Chart(document.getElementById('chart'), config)
  })
}


</script>

<template>
    <div class="main-chart-area mx-auto mt-100 w-[400px] h-[400px] bg-gray-400">
      <canvas id="chart">
      </canvas>
    </div>
  
    <div class="mt-20">
      <input type="text" v-model="newItem">
      <button @click="updateChart()" class="ml-2 bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded">
        Add
      </button>
  
    </div>
  </template>


<style scoped >
.main-chart-area{
 margin-top: 200px;

}
</style>