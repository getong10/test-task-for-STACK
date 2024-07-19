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
      v-if="props.labelInput==='filter'"
      :placeholder="props.placeholderInput"
      @input="$emit('update:modelValue', $event.target.value)"
  />

  <input
      v-if="props.labelInput==='company'"
      :placeholder="props.placeholderInput"
      @input="$emit('update:modelValue', $event.target.value)"
  />

  <input
      v-if="props.labelInput==='number'"
      :placeholder="props.placeholderInput"
      @input="$emit('update:modelValue', $event.target.value)"
  />

  <input
      v-if="props.labelInput==='name'"
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
