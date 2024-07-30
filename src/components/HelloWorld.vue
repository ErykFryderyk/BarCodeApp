<script setup>
import TheBarcode from './TheBarcode.vue';
import { ref } from 'vue'
import Vue3Barcode from 'vue3-barcode'


defineProps({
  msg: String,
})
</script>

<template>
  <h1>Hello world</h1>
  <!-- <vue3-barcode value="LA89005W20KR" :height="50" :width="1" /> -->
</template>

<style scoped>
</style>
