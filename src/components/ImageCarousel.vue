<script setup>
import { ref, reactive, onMounted, onBeforeUnmount, nextTick } from "vue";

const items = ref([
  {
    title: "Echoes of Time: Memories that Inspire",
    url: "https://images.unsplash.com/photo-1691859325266-5f812fcf81ff?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1975&q=80",
  },
  {
    title: "Floral Haven: Bridging Hearts and Homes",
    url: "https://images.unsplash.com/photo-1682685797742-42c9987a2c34?ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80",
  },
  {
    title: "Life's Service: Navigating the Unknown",
    url: "https://images.unsplash.com/photo-1682685797366-715d29e33f9d?ixlib=rb-4.0.3&ixid=M3wxMjA3fDF8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1170&q=80",
  },
  {
    title: "Perseverance Across Eras: Finding Solace",
    url: "https://plus.unsplash.com/premium_photo-1690446955129-7248ac32faaa?ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxwaG90by1wYWdlfHx8fGVufDB8fHx8fA%3D%3D&auto=format&fit=crop&w=1179&q=80",
  },
]);

let carousel = null;

onMounted(() => {
  carousel = new Flickity("#carousel", {});
  console.log("onMounted");
});

onBeforeUnmount(() => {
  carousel.destroy();
  console.log("Before Unmounted all data cleanup done");
});

let newItem = reactive({
  title: "",
  url: "",
});

function updateCarousel() {
  items.value.push(newItem);
  console.log(items);
  carousel.destroy();

  nextTick(() => {
    carousel = new Flickity("#carousel", {});
  });
}
</script>
<template>
  <form>
    <div class="grid gap-6 mb-6 md:grid-cols-3">
      <div>
        <input
          v-model="newItem.url"
          type="text"
          id="color-name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          required
          placeholder="Image URL"
        />
      </div>
      <div>
        <input
          v-model="newItem.title"
          type="text"
          id="color-name"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          required
          placeholder="Title"
        />
      </div>

      <div>
        <button
          @click.prevent="updateCarousel()"
          type="submit"
          class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-lg text-sm w-full sm:w-auto px-5 py-2.5 text-center dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
        >
          Add to Carousel
        </button>
      </div>
    </div>
  </form>
  <div class="mx-auto items" id="carousel">
    <div
      class="item"
      :style="`background-image:url(${item.url})`"
      v-for="(item, index) in items"
      :key="index"
    >
      <p class="pl-12 pr-12 pt-80 text-white font-bold">{{ item.title }}</p>
    </div>
  </div>
</template>

<style scoped>
.items {
  width: 1000px;
  height: 400px;
}

.item {
  width: 1000px;
  height: 400px;
  background-color: gray;
  background-size: cover;
}
</style>
