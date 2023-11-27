<template>
<SignUpForm :onSubmit="handleSubmit"/>
<ModalBox v-if="isOpen"  @close="closeModal" :data="data"/> 
</template>

<script setup>
import ModalBox from './components/ModalBox.vue';
import SignUpForm from './components/SignUpForm.vue';
import { ref } from 'vue';

const data = ref({})
const isOpen = ref(false);

function handleSubmit(formData){
  data.value = formData;
  isOpen.value = true;
}

function closeModal(){
  isOpen.value = false;
}
</script>

<style>
#app {
  font-family: 'Roboto', sans-serif;
  font-weight: 400;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  margin-top: 60px;
}

body{
  margin: 0;
  background: #eee;
}

.material-symbols-rounded {
  font-variation-settings:
  'FILL' 1,
  'wght' 400,
  'GRAD' 0,
  'opsz' 24
}
</style>
