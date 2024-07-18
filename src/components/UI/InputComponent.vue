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
      id="filter"
      :placeholder="props.placeholderInput"
      @input="$emit('update:modelValue', $event.target.value)"
  />

  <input
      v-if="props.labelInput===''"
      id="filter"
      @input="$emit('update:modelValue', $event.target.value)"
  />

  <input
      v-if="props.labelInput===''"
      id="filter"
      @input="$emit('update:modelValue', $event.target.value)"
  />
</template>

<style scoped>
#filter {
  padding: 2vh;
  cursor: pointer;
  border: 2px solid rgb(160, 160, 160);
}
</style>
