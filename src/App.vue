<script setup>
import { ref } from "vue";
import Carousel from "./components/ImageCarousel.vue";
import PieChart from "./components/PieChart.vue";

const toggle = ref(false);
console.log(toggle.value);
</script>

<template>
  <button @click="toggle = true">Carousel</button>
  <button @click="toggle = false">Pie Chart</button>

  <Carousel v-if="toggle == true"></Carousel>
  <PieChart v-if="!toggle"></PieChart>
</template>

<style scoped></style>
