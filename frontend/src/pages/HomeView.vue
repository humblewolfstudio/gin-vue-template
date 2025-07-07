<script setup lang="ts">
import {onMounted} from "vue";

const testApi = async () => {
  try {
    await fetch('/api/status')
  } catch (err) {
    console.error("Error fetching buckets:", err);
  }
};

onMounted(() => {
  testApi();
});
</script>

<template>
  <h1>Main View</h1>
</template>

<style scoped>

</style>