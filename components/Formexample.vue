<script setup lang="ts">
import { ref } from "vue";

const email = ref("");
const userCount = ref(10);

const handleSubmit = (event: Event) => {
  event.preventDefault();
  console.log("Opprett bruker med e-post:", email.value);
  alert("Opprettet bruker: " + email.value);
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
      <button type="submit" border bg="gray-100" mt="1" pl="1" pr="1">
        Opprett bruker
      </button>
    </form>
  </div>
</template>
