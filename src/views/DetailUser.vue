<script setup>
import axios from "axios";
import { onMounted, ref } from "vue";
import { useRoute } from "vue-router";

const route = useRoute();

const userId = route.params.id;

const user = ref({});

onMounted(async () => {
  try {
    const response = await axios.get(
      `https://jsonplaceholder.typicode.com/users/${userId}`
    );
    user.value = response.data;
  } catch (error) {
    console.error("Error fetching jobs", error);
  } finally {
    state.isLoading = false;
  }
});
</script>

<template>
  <div class="container mx-auto p-6">
    <div
      class="bg-white border border-gray-200 rounded-lg shadow-lg p-6 w-3/4 mx-auto"
    >
      <div class="mb-6">
        <button
          class="bg-blue-500 text-white px-4 py-2 rounded shadow hover:bg-blue-600"
        >
          Go Back
        </button>
      </div>
      <h1 class="text-2xl font-bold text-slate-800 mb-4">User Details</h1>

      <div class="grid grid-cols-1 sm:grid-cols-2 gap-4">
        <div>
          <h2 class="text-lg font-semibold text-slate-700">
            Personal Information
          </h2>
          <p class="text-slate-600"><strong>Name:</strong> {{ user.name }}</p>
          <p class="text-slate-600">
            <strong>Username:</strong> {{ user.username }}
          </p>
          <p class="text-slate-600"><strong>Email:</strong> {{ user.email }}</p>
          <p class="text-slate-600"><strong>Phone:</strong> {{ user.phone }}</p>
          <p class="text-slate-600">
            <strong>Website:</strong>
            <a href="#" class="text-blue-500 underline">{{ user.website }}</a>
          </p>
        </div>

        <div>
          <h2 class="text-lg font-semibold text-slate-700">Address</h2>
          <p class="text-slate-600">
            <strong>Street:</strong> {{ user.address.street }}
          </p>
          <p class="text-slate-600">
            <strong>Suite:</strong> {{ user.address.suite }}
          </p>
          <p class="text-slate-600">
            <strong>City:</strong> {{ user.address.city }}
          </p>
          <p class="text-slate-600">
            <strong>Zipcode:</strong> {{ user.address.zipcode }}
          </p>
        </div>

        <div>
          <h2 class="text-lg font-semibold text-slate-700">Geo Location</h2>
          <p class="text-slate-600">
            <strong>Latitude:</strong> {{ user.address.geo.lat }}
          </p>
          <p class="text-slate-600">
            <strong>Longitude:</strong> {{ user.address.geo.lng }}
          </p>
        </div>

        <div>
          <h2 class="text-lg font-semibold text-slate-700">Company</h2>
          <p class="text-slate-600">
            <strong>Name:</strong> {{ user.company.name }}
          </p>
          <p class="text-slate-600">
            <strong>Catchphrase:</strong> {{ user.company.catchPhrase }}
          </p>
          <p class="text-slate-600">
            <strong>Business:</strong> {{ user.company.bs }}
          </p>
        </div>
      </div>
    </div>
  </div>
</template>
