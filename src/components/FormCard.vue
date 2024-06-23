<template>
  <div class="rounded bg-flixGrey py-10 px-12 text-left">
    <div class="px-6 py-4">
      <div class="text-3xl font-bold underline text-flixBlack">IP Geo Lookup</div>
      <p class="text-flixBlack ">
        send a request to <a class="underline text-flixGreen" rel="noreferrer" href='http://ip-api.com/' target='_blank'>ip-api.com</a>
      </p>
    </div>
    <!-- Platz für Input-Komponenten -->
    <InputField :ip="ip" @updateIp="updateIp" @lookup="handleLookup" />
    <LoadingButton :loading="loading" @click="handleLookup" />
    <ErrorDisplay :error="error" />
    <DataDisplay :data="data" />
  </div>
</template>

<script setup>
import { ref } from 'vue';
import InputField from './InputField.vue';
import LoadingButton from './LoadingButton.vue';
import ErrorDisplay from './ErrorDisplay.vue';
import DataDisplay from './DataDisplay.vue';
import axios from 'axios';

const ip = ref('');
const data = ref(null);
const loading = ref(false);
const error = ref(null);

const ipv4Regex = /^(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)\.(25[0-5]|2[0-4][0-9]|[01]?[0-9][0-9]?)$/;
const ipv6Regex = /^(?:[a-fA-F0-9]{1,4}:){7}[a-fA-F0-9]{1,4}$/;

const isValidIP = (ip) => ipv4Regex.test(ip) || ipv6Regex.test(ip);

const updateIp = (newIp) => {
  ip.value = newIp;
  data.value = null;
  error.value = null;
};

const handleLookup = async () => {
  if (!isValidIP(ip.value)) {
    error.value = 'Invalid IP address';
    return;
  }
  error.value = null;
  loading.value = true;
  try {
    const response = await axios.post('http://localhost:4000/api/lookup', { ip: ip.value });
    data.value = response.data;
  } catch (err) {
    console.error(err);
    error.value = 'An error occurred';
  } finally {
    loading.value = false;
  }
};
</script>

