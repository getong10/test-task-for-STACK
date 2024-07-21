<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  msgProps: String,
  type: String,
  modelValue: Boolean
});

</script>

<template>
  <button v-if="props.type === 'add'" id="add" @click="$emit('update:modelValue', true)">
    {{ props.msgProps }}
  </button>

  <button v-if="props.type === 'delete'" id="delete">
    {{ props.msgProps }}
  </button>

  <button v-if="props.type === 'confirm'" id="confirm" @click="$emit('update:modelValue', false)">
    {{ props.msgProps }}
  </button>

  <button v-if="props.type === 'cancel'" id="cancel" @click="$emit('update:modelValue', false)">
    {{ props.msgProps }}
  </button>
</template>

<style scoped>
#add, #cancel, #confirm, #delete {
  color: rgb(255, 255, 255);
  padding: 1vh 1vw;
  font-size: 1rem;
  border: none;
  cursor: pointer;
}

#add {
  background-color: rgb(66, 104, 255);
  padding: 2vh 2vw;
}

#confirm {
  background-color: rgb(66, 104, 255);
}

#cancel {
  background-color: rgb(230, 9, 9);
}

#delete {
  margin: 2px;
  background-color: rgb(230, 9, 9);
}

</style>
