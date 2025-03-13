<template>
  <div class="min-h-screen bg-gray-100">
    <!-- Верхняя навигационная панель -->
    <header class="bg-white shadow-md p-4">
      <div class="container mx-auto flex justify-between items-center">
        <div class="p-2">
          <span class="text-lg font-bold">neuro-spam</span>
        </div>
        
        <nav class="flex-1 mx-10">
          <ul class="flex items-center">
            <li class="text-gray-900 font-medium cursor-pointer mr-6">Проекты</li>
            <li class="text-gray-700 hover:text-gray-900 cursor-pointer relative">
              Уведомления
              <span class="absolute -top-2 -right-2 bg-red-500 text-white text-xs rounded-full w-5 h-5 flex items-center justify-center">3</span>
            </li>
          </ul>
        </nav>
        
        <div class="relative">
          <div 
            class="cursor-pointer hover:bg-gray-100 p-2 rounded-lg"
            @click="toggleProfileMenu"
          >
            <span class="font-medium">Профиль</span>
          </div>
          
          <!-- Выпадающее меню -->
          <div 
            v-if="showProfileMenu" 
            class="absolute right-0 mt-2 bg-white rounded-lg shadow-lg p-2 w-48 z-10"
          >
            <div class="py-2 px-4 hover:bg-gray-100 cursor-pointer rounded">
              Мой профиль
            </div>
            <div class="py-2 px-4 hover:bg-gray-100 cursor-pointer rounded">
              Настройки
            </div>
            <div class="py-2 px-4 hover:bg-gray-100 cursor-pointer rounded text-red-600">
              Выйти
            </div>
          </div>
        </div>
      </div>
    </header>
    
    <!-- Основное содержимое -->
    <main class="container mx-auto py-8 px-4">
      <h1 class="text-3xl font-bold mb-8">Проекты</h1>
      
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-6">
        <!-- Карточки рассылок -->
        <div v-for="i in 6" :key="i" class="bg-white rounded-lg shadow-md p-6 border border-gray-300">
          <h3 class="text-xl font-semibold mb-4">Рассылка №{{ i }}</h3>
          <div class="space-y-2">
            <p class="text-gray-700">Кол-во сообщений: N</p>
            <p class="text-gray-700">Конверсия: X%</p>
          </div>
        </div>
      </div>
    </main>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const showProfileMenu = ref(false);

const toggleProfileMenu = () => {
  showProfileMenu.value = !showProfileMenu.value;
};

// Закрываем меню при клике вне меню
if (process.client) {
  window.addEventListener('click', (e) => {
    if (!e.target.closest('.profile-menu') && !e.target.closest('.profile-trigger')) {
      showProfileMenu.value = false;
    }
  });
}
</script>

<style scoped>
/* Дополнительные стили */
</style> 