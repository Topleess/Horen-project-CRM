<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-100 flex-col">
    <h1 v-if="isLoading" class="text-2xl mb-4">Загрузка приложения...</h1>
    <div v-if="isLoading" class="animate-spin rounded-full h-12 w-12 border-b-2 border-gray-900"></div>
    
    <div v-if="error" class="bg-white p-6 rounded-lg shadow-lg max-w-md text-center">
      <h2 class="text-xl font-bold mb-4 text-red-600">Произошла ошибка</h2>
      <p class="mb-4">{{ error }}</p>
      <button 
        @click="retryRedirect" 
        class="bg-blue-600 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded-lg"
      >
        Попробовать снова
      </button>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';

const router = useRouter();
const isLoading = ref(true);
const error = ref(null);

const navigateToAuth = async () => {
  // Прямое перенаправление с помощью window.location
  // Это обходит любые проблемы с роутером Vue
  window.location.href = '/auth';
};

const retryRedirect = () => {
  isLoading.value = true;
  error.value = null;
  setTimeout(navigateToAuth, 500);
};

onMounted(() => {
  // Меньшая задержка для более быстрого редиректа
  setTimeout(navigateToAuth, 300);
});
</script> 