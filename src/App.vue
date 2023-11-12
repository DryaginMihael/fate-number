<template>
  <div class="flex flex-col items-center justify-center h-screen max-w-screen-md">
    <h2 class="text-2xl font-bold mb-4">Нумерологический калькулятор</h2>
    <form @submit.prevent="calculateNumber" class="mb-4">
      <label for="birthdate" class="mr-2">Дата рождения:</label>
      <input type="date" id="birthdate" v-model="birthdate" required class="border rounded p-2 text-black">
      <button type="submit" class="bg-blue-900 ml-2 text-white py-2 px-4 border border-blue-900 border-2 rounded hover:bg-blue-800">Рассчитать</button>
    </form>
    <div v-if="age !== null" class="text-xl">
      <p>Ваш возраст: {{ age }} лет</p>
    </div>
    <PredictionText
      v-if="magicNumber"
      :number="magicNumber">
    </PredictionText>
  </div>
</template>

<script setup>
import { ref } from 'vue';
import PredictionText from './components/PredictionText.vue';

const birthdate = ref('');
const age = ref(null);

const magicNumber = ref(null);

const calculateNumber = () => {
  if (birthdate.value) {
    const birthDate = new Date(birthdate.value);

    const year = birthDate.getFullYear();
    const month = birthDate.getMonth() + 1;
    const day = birthDate.getDate();

    let str = '' + year + month + day;
    while (str.length > 1) {
      str = '' + str.split('')
        .map(item => +item)
        .reduce((acc, item) => acc + item, 0)
    }
    magicNumber.value = +str;
  }
}

const calculateAge = () => {
  if (birthdate.value) {
    const birthDate = new Date(birthdate.value);
    const currentDate = new Date();
    const yearsDiff = currentDate.getFullYear() - birthDate.getFullYear();

    if (
      currentDate.getMonth() < birthDate.getMonth() ||
      (currentDate.getMonth() === birthDate.getMonth() &&
        currentDate.getDate() < birthDate.getDate())
    ) {
      age.value = yearsDiff - 1;
    } else {
      age.value = yearsDiff;
    }
  }
};
</script>

<style scoped>
/* Добавьте здесь свои стили, если необходимо */
</style>
