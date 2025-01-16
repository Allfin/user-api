<script setup>
import axios from "axios";
import { onMounted, reactive } from "vue";
import Button from "./ui/button/Button.vue";

const state = reactive({
  users: {},
  isLoading: true,
});

onMounted(async () => {
  try {
    const response = await axios.get(
      `https://jsonplaceholder.typicode.com/users`
    );
    state.users = response.data;
    console.log(JSON.stringify(state.users));
  } catch (error) {
    console.error("Error fetching jobs", error);
  } finally {
    state.isLoading = false;
  }
});
</script>

<template>
  <Button>Click Me</Button>
</template>
