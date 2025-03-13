<template>
  <div class="bg-white rounded-lg p-8 max-w-md w-full shadow-lg relative">
    <div class="absolute top-4 left-4">
      <div class="p-2">
        <span class="text-lg font-bold">neuro-spam</span>
      </div>
    </div>
    
    <div class="mb-8 mt-10">
      <h2 class="text-2xl font-bold text-center mb-2">
        <span 
          class="cursor-pointer" 
          :class="{ 'text-blue-600': !isLogin, 'opacity-50': isLogin }"
          @click="toggleAuthMode(false)"
        >
          Регистрация
        </span> 
        / 
        <span 
          class="cursor-pointer" 
          :class="{ 'text-blue-600': isLogin, 'opacity-50': !isLogin }"
          @click="toggleAuthMode(true)"
        >
          Авторизация
        </span>
      </h2>
    </div>
    
    <form @submit.prevent="submitForm">
      <div class="mb-4">
        <label class="block text-gray-700 mb-2">Введите e-mail</label>
        <input 
          type="email" 
          v-model="email" 
          class="input-field" 
          placeholder="e-mail" 
          required
        />
      </div>
      
      <div class="mb-6">
        <label class="block text-gray-700 mb-2">Введите пароль</label>
        <input 
          type="password" 
          v-model="password" 
          class="input-field" 
          placeholder="пароль" 
          required
        />
      </div>
      
      <button 
        type="submit" 
        class="bg-gray-600 text-white w-full py-3 rounded-lg hover:bg-gray-700 transition-all duration-300"
      >
        Продолжить
      </button>
    </form>
  </div>
</template>

<script setup>
import { ref } from 'vue';

const isLogin = ref(true);
const email = ref('');
const password = ref('');

const emit = defineEmits(['submit']);

const toggleAuthMode = (loginMode) => {
  isLogin.value = loginMode;
};

const submitForm = () => {
  emit('submit', {
    mode: isLogin.value ? 'login' : 'register',
    email: email.value,
    password: password.value
  });
};
</script> 