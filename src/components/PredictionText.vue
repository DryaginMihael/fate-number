<script setup>
// import { ref } from 'vue';
import predictions from './predictions';

// const prediction = ref('');

defineProps({
    number: {
        type: Number,
        required: false
    }
})

</script>

<template>
    <div class="flex flex-col items-center justify-center">
        <h2 class="text-2xl font-bold mb-4">Ваше число судьбы: {{ number }}</h2>
        {{ number ? predictions[number - 1] : '' }}
    </div>
</template>