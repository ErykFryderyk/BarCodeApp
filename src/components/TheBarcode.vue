<script setup>
import { onMounted, ref, watch } from 'vue';
import JsBarcode from 'jsbarcode';

const props = defineProps({
    value: {
      type: String,
      required: true
    },
    format: {
      type: String,
      default: 'CODE128'
    },
    fontSize: {
      type: Number,
      default: 10
    },
    lineColor: {
      type: String,
      default: '#000'
    },
    width: {
      type: Number,
      default: 1
    },
    height: {
      type: Number,
      default: 25
    },
    displayValue: {
      type: Boolean,
      default: true
    }
})
const barcode = ref(null);

const renderBarcode = () => {
  JsBarcode(barcode.value, props.value, {
    format: props.format,
    fontSize: props.fontSize,
    lineColor: props.lineColor,
    width: props.width,
    height: props.height,
    displayValue: props.displayValue
  });
};

onMounted(renderBarcode);

watch(() => props.value, renderBarcode);
</script>
<template>
    <div class="">
        <svg ref="barcode"></svg>
    </div>
</template>
