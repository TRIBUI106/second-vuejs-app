<template>

<button class="btn btn-primary" @click="">Plus 1</button>

</template>

<script setup>

import { ref, watchEffect } from 'vue';

const count = ref(0);

</script>