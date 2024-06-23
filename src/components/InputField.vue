<template>
  <input
    name="ip_adress"
    class="rounded-lg border-none py-2 px-4 text-xl"
    type="text"
    :value="ip"
    @input="handleChange"
    @keydown.enter="handleLookup"
    placeholder="Enter IP address"
  />
</template>

<script setup>
import { ref, defineEmits, defineProps, watch } from 'vue';

const props = defineProps({
  ip: String,
});

const emit = defineEmits(['updateIp', 'lookup']);

const input = ref(props.ip);

watch(() => props.ip, (newIp) => {
  input.value = newIp;
});

const handleChange = (event) => {
  emit('updateIp', event.target.value);
};

const handleLookup = () => {
  emit('lookup');
};
</script>

