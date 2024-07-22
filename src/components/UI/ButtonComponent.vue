<script setup>
import { defineProps, defineEmits } from 'vue';

const props = defineProps({
  msgProps: String,
  type: String,
  check: Boolean
});

const emit = defineEmits(['click']);

const handleClick = (event) => {
  emit('click', event);
};
</script>

<template>
  <button
      v-if="props.type==='confirm'||props.type==='pagination'"
      :id="props.check?'confirm':'disabled'"
      @click="handleClick"
      :disabled="!props.check"
  >
    {{ props.msgProps }}
  </button>

  <button
      v-else
      :id="props.type"
      @click="handleClick"
  >
    {{ props.msgProps }}
  </button>
</template>

<style scoped>
#add, #cancel, #confirm, #delete, #disabled, #pagination {
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

#confirm, #pagination {
  background-color: rgb(66, 104, 255);
}

#disabled {
  background-color: rgb(219,219,219);
  color: rgb(1, 1, 1);
  cursor: default;
}

#cancel {
  background-color: rgb(230, 9, 9);
}

#delete {
  margin: 2px;
  background-color: rgb(230, 9, 9);
}

</style>