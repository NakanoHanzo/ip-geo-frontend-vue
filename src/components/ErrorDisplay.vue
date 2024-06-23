<template>
  <p v-if="error" class="text-red">{{ error }}</p>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  error: String,
});
</script>
