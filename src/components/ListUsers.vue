<script setup>
import axios from "axios";
import { onMounted, reactive } from "vue";
import {
  Table,
  TableBody,
  TableCaption,
  TableCell,
  TableHead,
  TableHeader,
  TableRow,
} from "@/components/ui/table";
import { useRouter } from "vue-router";

const router = useRouter();

const state = reactive({
  users: {},
  isLoading: true,
});

const handleDetailUser = (userId) => {
  router.push(`/users/${userId}`);
};

onMounted(async () => {
  try {
    const response = await axios.get(
      `https://jsonplaceholder.typicode.com/users`
    );
    state.users = response.data;
  } catch (error) {
    console.error("Error fetching jobs", error);
  } finally {
    state.isLoading = false;
  }
});
</script>

<template>
  <div class="container mx-auto p-4">
    <h1 class="text-2xl font-bold mb-4">User Table</h1>
    <Table
      class="table-auto w-full border-collapse border border-gray-200 rounded-lg"
    >
      <TableCaption>List User</TableCaption>
      <TableHeader class="bg-slate-100">
        <TableRow>
          <TableHead class="border border-gray-300 px-4 py-2 text-left">
            Nama
          </TableHead>
          <TableHead class="border border-gray-300 px-4 py-2 text-left"
            >Email</TableHead
          >
          <TableHead class="border border-gray-300 px-4 py-2 text-left"
            >Alamat</TableHead
          >
        </TableRow>
      </TableHeader>
      <TableBody>
        <TableRow
          v-for="user in state.users"
          :key="user.id"
          class="hover:bg-slate-50"
          @click="handleDetailUser(user.id)"
        >
          <TableCell class="border border-gray-300 px-4 py-2">
            {{ user.username }}
          </TableCell>
          <TableCell class="border border-gray-300 px-4 py-2">{{
            user.email
          }}</TableCell>
          <TableCell class="border border-gray-300 px-4 py-2">
            {{ user.address.street }}, {{ user.address.city }}</TableCell
          >
        </TableRow>
      </TableBody>
    </Table>
  </div>
</template>
