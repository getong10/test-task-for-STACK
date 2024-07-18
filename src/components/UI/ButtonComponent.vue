<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  msgProps: String,
  type: String,
  modelValue: Boolean
})
</script>

<template>
  <button v-if="props.type==='add'" id="add" @click="$emit('update:modelValue', true)">
    {{ props.msgProps }}
  </button>

  <button v-if="props.type==='delete'" id="delete">
    {{ props.msgProps }}
  </button>

  <button v-if="props.type==='confirm'" id="confirm">
    {{ props.msgProps }}
  </button>

  <button v-if="props.type==='cancel'" id="cancel">
    {{ props.msgProps }}
  </button>
</template>

<style scoped>
  #add {
    background-color: rgb(66, 104, 255);
    padding: 2vh 2vw;
    color: aliceblue;
    font-weight: bold;
    font-size: 1.1rem;
    border: none;
    cursor: pointer;
  }

  #delete {
    margin: 2px;
    background-color: rgb(230, 9, 9);
    color: aliceblue;
    border: none;
    cursor: pointer;
  }
</style>
