<script setup>
import { ref, onMounted } from "vue";
import axios from "axios";
import CategoriesCard from "@/components/CategoriesCard.vue";

// const categories = ref([
//   { id: 1, title: "Mobile UI Kit", count: "123" },
//   { id: 2, title: "Web UI Kit", count: "345" },
//   { id: 3, title: "WordPress UI Kit", count: "567" },
//   { id: 4, title: "Icon UI Kit", count: "890" },
// ]);

const categories = ref([]);

async function getCategoriesData() {
  try {
    const response = await axios.get(
      "https://zullkit-backend.demo.belajarkoding.com/api/categories?limit=4&show_product="
    );
    categories.value = response.data.data.data;
  } catch (error) {
    console.error(error);
  }
}

onMounted(() => {
  getCategoriesData();
});
</script>

<template>
  <div class="container px-4 mx-auto my-16 md:px-12">
    <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">Top Categories</h2>
    <div class="flex flex-wrap -mx-1 lg:-mx-4">
      <CategoriesCard
        v-for="category in categories"
        :key="category.id"
        :title="category.name"
        :count="category.products_count"
        :image="category.thumbnails"
        :id="category.id" />
    </div>
  </div>
</template>

<style></style>
