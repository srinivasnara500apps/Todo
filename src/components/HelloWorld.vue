
<script setup>
import { ref } from 'vue'

const message = ref('Hello World!')
</script>

<template>
  <h1 class="bg-blue-300">{{ message }}</h1>
</template>