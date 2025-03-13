<template>
  <div>
    <NuxtPage />
  </div>
</template>

<script setup>
import { onMounted, onErrorCaptured, ref } from 'vue';

const error = ref(null);

// Обработка ошибок на уровне приложения
onErrorCaptured((err, instance, info) => {
  console.error('Перехвачена ошибка в приложении:', err);
  error.value = err;
  return false; // не пропускать ошибку дальше
});

onMounted(() => {
  console.log('Приложение загружено');
});
</script>

<style>
body {
  font-family: 'Inter', system-ui, -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, 'Helvetica Neue', Arial, sans-serif;
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

/* Базовые стили для приложения */
.input-field {
  @apply border border-gray-300 rounded-lg py-2 px-4 w-full focus:outline-none focus:ring-2 focus:ring-blue-600 focus:border-transparent;
}
</style>
