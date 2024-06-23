<template>
  <div v-if="data">
    <div v-for="(value, key) in data" :key="key">
      <strong>{{ key.charAt(0).toUpperCase() + key.slice(1) }}:</strong> {{ value }}
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  data: Object,
});
</script>
