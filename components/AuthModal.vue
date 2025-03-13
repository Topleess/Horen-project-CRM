<template>
  <div v-if="isOpen" class="fixed inset-0 flex items-center justify-center z-50">
    <div class="absolute inset-0 bg-black opacity-50" @click="closeModal"></div>
    <div class="bg-white rounded-lg p-8 max-w-md w-full relative z-10 shadow-xl">
      <h2 class="text-2xl font-bold mb-6 text-center">Выберите тип пользователя</h2>
      
      <div class="grid grid-cols-2 gap-4">
        <button 
          class="bg-gray-600 hover:bg-gray-700 text-white p-4 rounded-lg flex flex-col items-center justify-center transition-all duration-300"
          @click="selectRole('user')"
        >
          <span class="text-3xl mb-2">👤</span>
          <span class="font-medium">Пользователь</span>
        </button>
        
        <button 
          class="bg-gray-600 hover:bg-gray-700 text-white p-4 rounded-lg flex flex-col items-center justify-center transition-all duration-300"
          @click="selectRole('admin')"
        >
          <span class="text-3xl mb-2">👑</span>
          <span class="font-medium">Администратор</span>
        </button>
      </div>
      
      <button 
        class="absolute top-2 right-2 text-gray-500 hover:text-gray-700"
        @click="closeModal"
      >
        <span class="text-2xl">&times;</span>
      </button>
    </div>
  </div>
</template>

<script setup>
const props = defineProps({
  isOpen: {
    type: Boolean,
    default: false
  }
});

const emit = defineEmits(['close', 'selectRole']);

const closeModal = () => {
  emit('close');
};

const selectRole = (role) => {
  console.log('Роль выбрана:', role);
  emit('selectRole', role);
  closeModal();
};
</script> 