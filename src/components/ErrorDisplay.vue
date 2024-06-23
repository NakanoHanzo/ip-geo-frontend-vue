<template>
  <p v-if="error" class="text-red standard-text">{{ error }}</p>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  error: String,
});
</script>
