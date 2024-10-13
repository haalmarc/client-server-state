<script setup lang="ts">
import { ref } from "vue";

const email = ref("");
const userCount = ref(10);
const loading = ref(false);

const handleSubmit = (event: Event) => {
  event.preventDefault();
  loading.value = true;

  // Simulerer loading i 3 sekunder
  setTimeout(() => {
    userCount.value += 1;
    loading.value = false;
  }, 3000);
};
</script>

<template>
  <div p="4" border>
    <h3>Opprett ny bruker</h3>
    <p>Antall brukere: {{ userCount }}</p>

    <form @submit="handleSubmit">
      <label>
        E-post:
        <input v-model="email" border />
      </label>
      <br />
      <button
        type="submit"
        border
        bg="gray-300"
        text="black"
        mt="1"
        pl="1"
        pr="1"
        :disabled="loading"
      >
        {{ loading ? "Laster..." : "Opprett bruker" }}
      </button>
    </form>
  </div>
</template>
