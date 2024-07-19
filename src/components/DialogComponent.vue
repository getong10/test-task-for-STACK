<script setup>

import InputComponent from "@/components/UI/InputComponent.vue";
import ButtonComponent from "@/components/UI/ButtonComponent.vue";
import { ref } from "vue";

const model = ref({
  CompanyName: '',
  PhoneNumber: '',
  DirectorName: ''
})
</script>

<template>
  <div id="container">
    <div id="modal">
      <h4>Добавить организацию</h4>
      <input-component
          labelInput="company"
          placeholderInput="Название"
          v-model="model.CompanyName"
      />
      <input-component
          labelInput="number"
          placeholderInput="Номер телефона"
          v-model="model.PhoneNumber"
      />
      <input-component
          labelInput="name"
          placeholderInput="ФИО директора"
          v-model="model.DirectorName"
      />
      <div id="actions">
        <button-component msgProps="Отмена" type="cancel"/>
        <button-component msgProps="ОК" type="confirm"/>
      </div>
    </div>
  </div>
</template>

<style scoped>
#container {
  background-color: rgba(0, 0, 0, 30%);
  width: 100%;
  height: 100%;
  position: absolute;
  overflow: hidden;
  display: flex;
  justify-content: center;
  align-items: center;
}

#modal {
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: rgb(255, 255, 255);
  gap: 10px;
  padding: 10px;
}

h4 {
  font-family: sans-serif;
  font-size: 1rem;
}

#actions {
  display: flex;
  justify-content: space-between;
  align-items: center;
  width: 100%;
}
</style>
