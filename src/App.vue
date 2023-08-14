<script setup>
import { ref } from "vue";
import Carousel from "./components/ImageCarousel.vue";
import PieChart from "./components/PieChart.vue";

const toggle = ref(true);
console.log(toggle.value);
</script>

<template>
  <div class="mb-5">
    <h1 class="mb-5 text-3xl">Welcome!</h1>
    <button class="bg-blue-600 text-white mr-2" @click="toggle = true">
      Carousel
    </button>
    <button class="bg-blue-600 text-white" @click="toggle = false">
      Pie Chart
    </button>
  </div>
  <div>
    <Carousel v-if="toggle == true"></Carousel>
    <PieChart v-if="!toggle"></PieChart>
  </div>
</template>

<style scoped></style>
