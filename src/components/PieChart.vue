<script setup>
import { onBeforeMount, onMounted, onBeforeUnmount, ref } from "vue";

let pieChart = null;
let doughnutChart = null;

const data = {
  labels: ["Red", "Blue", "Yellow"],
  datasets: [
    {
      data: [300, 50, 100],
      backgroundColor: [
        "rgb(255, 99, 132)",
        "rgb(54, 162, 235)",
        "rgb(255, 205, 86)",
      ],
      hoverOffset: 4,
    },
  ],
};

const pieConfig = {
  type: "pie",
  data: data,
  options: {
    responsive: true,
  },
};

const doughnutConfig = {
  type: "doughnut",
  data: data,
  options: {
    responsive: true,
  },
};

onBeforeMount(() => {
  console.log("Before Mounted");
});

onMounted(() => {
  const pieCtx = document.getElementById("myPieChart").getContext("2d");
  const doughnutCtx = document
    .getElementById("myDoughnutChart")
    .getContext("2d");

  pieChart = new Chart(pieCtx, pieConfig);
  doughnutChart = new Chart(doughnutCtx, doughnutConfig);
});

onBeforeUnmount(() => {
  pieChart.destroy();
  doughnutChart.destroy();
  console.log("Before Unmounted all data cleanup done");
});

const colorName = ref("");
const colorParcent = ref("");

function updateChart() {
  data.labels.push(colorName.value);
  data.datasets[0].data.push(colorParcent.value);
  data.datasets[0].backgroundColor.push(colorName.value.toLowerCase());

  pieChart.update();
  doughnutChart.update();
}
</script>

<template>
  <form>
    <div class="grid gap-6 mb-6 md:grid-cols-3">
      <div>
        <input
          v-model="colorName"
          type="text"
          id="color-name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          required
          placeholder="Color Name"
        />
      </div>
      <div>
        <input
          v-model="colorParcent"
          type="number"
          id="color-parcent"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          required
          placeholder="Value"
        />
      </div>
      <div>
        <button
          @click.prevent="updateChart()"
          type="submit"
          class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
        >
          Add to Chart
        </button>
      </div>
    </div>
  </form>
  <div class="grid grid-cols-2 gap-6">
    <div class="w-2/3">
      <h1 class="text-2xl text-gray-900 text-center">Pie Chart</h1>
      <canvas id="myPieChart"></canvas>
    </div>
    <div class="w-2/3">
      <h1 class="text-2xl text-gray-900 text-center">Doughnut Chart</h1>
      <canvas id="myDoughnutChart"></canvas>
    </div>
  </div>
</template>

<style scoped></style>
