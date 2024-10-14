<script setup lang="ts">
import { ref } from "vue";

const email = ref("");
const errorMessage = ref("");
const userCount = ref(10);
const loading = ref(false);
const shouldSucceed = ref(true);
const previousUserCount = ref<number | null>(null);

const handleSubmit = (event: Event) => {
  event.preventDefault();
  errorMessage.value = "";

  // Simulerer optimistisk oppdatering ved umiddelbart å øke brukertallet
  previousUserCount.value = userCount.value;
  userCount.value += 1;
  loading.value = true;

  setTimeout(() => {
    if (!shouldSucceed.value) {
      userCount.value = previousUserCount.value;
      errorMessage.value = "En feil skjedde.";
    }
    shouldSucceed.value = !shouldSucceed.value;
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
      <p>{{ errorMessage }}</p>
    </form>
  </div>
</template>
