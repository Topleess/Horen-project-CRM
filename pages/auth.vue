<template>
  <div class="min-h-screen flex items-center justify-center p-4 bg-gray-100">
    <!-- Индикатор загрузки при попытке перенаправления -->
    <div v-if="isLoading" class="fixed inset-0 flex items-center justify-center bg-black bg-opacity-50 z-50">
      <div class="bg-white p-6 rounded-lg shadow-xl flex flex-col items-center">
        <div class="animate-spin rounded-full h-12 w-12 border-b-2 border-gray-900 mb-4"></div>
        <p class="text-lg">Выполняется вход...</p>
      </div>
    </div>
    
    <AuthForm @submit="handleAuthSubmit" />
    
    <AuthModal 
      :is-open="isModalOpen" 
      @close="closeModal" 
      @select-role="handleRoleSelect" 
    />
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { useRouter } from 'vue-router';
import AuthForm from '~/components/AuthForm.vue';
import AuthModal from '~/components/AuthModal.vue';

const router = useRouter();
const isModalOpen = ref(false);
const authData = ref(null);
const isLoading = ref(false);

const handleAuthSubmit = (data) => {
  authData.value = data;
  isModalOpen.value = true;
};

const closeModal = () => {
  isModalOpen.value = false;
};

const handleRoleSelect = (role) => {
  console.log('Выбрана роль:', role);
  console.log('Данные авторизации:', authData.value);
  
  // Устанавливаем флаг загрузки
  isLoading.value = true;
  
  // Имитация авторизации
  setTimeout(() => {
    // Используем прямое перенаправление с window.location для надёжности
    try {
      if (role === 'user') {
        window.location.href = '/user-dashboard';
      } else if (role === 'admin') {
        window.location.href = '/admin-dashboard';
      }
    } catch (error) {
      console.error('Ошибка при перенаправлении:', error);
      alert('Произошла ошибка при перенаправлении. Пожалуйста, попробуйте снова.');
      isLoading.value = false;
    }
  }, 500);
};

// Проверим, что страница действительно загрузилась
onMounted(() => {
  console.log('Страница авторизации загружена');
});
</script> 