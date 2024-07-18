<script setup>
import ButtonComponent from "@/components/UI/ButtonComponent.vue";
import {defineProps} from "vue";

const props = defineProps({
  data: Array
})
</script>

<template>
  <div id="table">
    <div id="table-header">
      <div class="col-container">
        <div class="row-header">Название</div>
        <div class="row-header">ФИО директора</div>
        <div class="row-header">Номер телефона</div>
        <div class="row-header"></div>
      </div>
    </div>
    <div id="table-body">
      <div class="col-container" v-for="(record, index) in props.data" :key="index">
        <div class="row">{{ record.CompanyName }}</div>
        <div class="row">{{ record.DirectorName }}</div>
        <div class="row">{{ record.PhoneNumber }}</div>
        <button-component msgProps="X" type="delete"/>
      </div>
    </div>
  </div>
</template>

<style scoped>
#table {
  width: 70%;
  border: 2px solid rgb(140, 140, 140);
  font-family: sans-serif;
  font-size: 1rem;
}

.col-container {
  display: grid;
  grid-template-columns: 3fr 6fr 3fr 1fr;
}

.row-header, .row {
  border: 1px solid rgb(160, 160, 160);
  padding: 8px;
}

.row-header {
  font-weight: bold;
  font-size: 1.1rem;
  text-align: center;
}

.row {
  display: flex;
}

.row:nth-child(3) {
  justify-content: end;
}


</style>
