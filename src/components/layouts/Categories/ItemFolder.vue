<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import { useRoute } from "vue-router";
import ItemCard from "@/components/layouts/Categories/ItemCard.vue";

// const items = ref([
//   { id: 1, title: "Mobile UI Kit", category: "Mobile" },
//   { id: 2, title: "Web UI Kit", category: "Web" },
//   { id: 3, title: "WP UI Kit", category: "Wordpress" },
// ]);

const items = ref([]);
const category = ref({});
const route = useRoute();

async function getItemsData() {
  try {
    const response = await axios.get(
      "https://zullkit-backend.demo.belajarkoding.com/api/categories?id=" +
        route.params.id +
        "&show_product=1"
    );
    items.value = response.data.data.products;
    category.value = response.data.data;
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
    <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">
      {{ category.name }}
    </h2>
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
