<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import ItemCard from "@/components/ItemCard.vue";

// const items = ref([
//   { id: 1, title: "Mobile UI Kit", category: "Mobile" },
//   { id: 2, title: "Web UI Kit", category: "Web" },
//   { id: 3, title: "WP UI Kit", category: "Wordpress" },
// ]);

const items = ref([]);

async function getItemsData() {
  try {
    const response = await axios.get(
      "https://zullkit-backend.demo.belajarkoding.com/api/products"
    );
    items.value = response.data.data.data;
    console.log(response);
  } catch (error) {
    console.log(error);
  }
}

onMounted(() => {
  getItemsData();
});
</script>

<template>
  <div class="container px-4 mx-auto my-16 md:px-12">
    <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">New Items</h2>
    <div class="flex flex-wrap -mx-1 lg:-mx-4">
      <ItemCard
        v-for="item in items"
        :key="item.id"
        :title="item.name"
        :category="item.subtitle"
        :image="item.thumbnails"
        :id="item.id" />
    </div>
  </div>
</template>

<style></style>
