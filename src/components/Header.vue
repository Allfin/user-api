<script setup>
import { ref } from "vue";

const isMenuOpen = ref(false);
const searchQuery = ref("");
</script>

<template>
  <header class="bg-white shadow-md">
    <div class="container mx-auto flex items-center justify-between p-4">
      <div class="text-lg font-bold">User Api</div>

      <div class="relative">
        <input
          v-model="searchQuery"
          type="text"
          placeholder="Search..."
          class="border rounded-lg px-4 py-2 focus:outline-none focus:ring focus:border-blue-300"
        />
      </div>
    </div>
  </header>
</template>
