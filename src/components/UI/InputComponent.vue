<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  labelInput: String,
  placeholderInput: String,
  modelValue: String
})
</script>

<template>
  <input
      :placeholder="props.placeholderInput"
      @input="$emit('update:modelValue', $event.target.value)"
  />
</template>

<style scoped>
input {
  padding: 2vh;
  cursor: pointer;
  border: 2px solid rgb(160, 160, 160);
}
</style>