<script setup>

import data from '/src/data.json'
import TableComponent from "@/components/TableComponent.vue";
import ButtonComponent from "@/components/UI/ButtonComponent.vue";
import InputComponent from "@/components/UI/InputComponent.vue";
import {computed, ref} from "vue";
import DialogComponent from "@/components/DialogComponent.vue";

const filter = ref('')
const showDialog = ref(false)

const filterFn = computed(() => {
  return data.filter(item => item.DirectorName.toLowerCase().includes(filter.value.toLowerCase()))
})
</script>

<template>
  <dialog-component v-show="showDialog" />
  <div id="content">
    <div id="header">
      <input-component
          labelInput="filter"
          placeholderInput="Найти по ФИО..."
          v-model="filter"
      />
      <button-component msgProps="Добавить" type="add" v-model="showDialog"/>
    </div>
    <table-component :data="filterFn" />
  </div>
</template>

<style scoped>
#content {
  display: flex;
  align-items: center;
  flex-direction: column;
}

#header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 70%;
  margin: 50px 0 10px 0;
}
</style>
