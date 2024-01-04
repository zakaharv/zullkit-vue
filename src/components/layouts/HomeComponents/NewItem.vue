<script setup>
import { ref } from 'vue';
import ItemCard from '@/components/ItemCard.vue';

const items = ref([
    { id: 1, title: 'Mobile UI Kit', category: 'Mobile' },
    { id: 2, title: 'Web UI Kit', category: 'Web' },
    { id: 3, title: 'WP UI Kit', category: 'Wordpress' },
])
</script>

<template>
    <div class="container px-4 mx-auto my-16 md:px-12">
        <h2 class="mb-4 text-xl font-medium md:mb-0 md:text-lg">New Items</h2>
        <div class="flex flex-wrap -mx-1 lg:-mx-4">

            <ItemCard v-for="item in items" :key="item.id" :title="item.title" :category="item.category" />


        </div>
    </div>
</template>

<style></style>