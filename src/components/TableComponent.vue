<script setup>
import ButtonComponent from "@/components/UI/ButtonComponent.vue";
import {defineProps, defineEmits, ref} from "vue";

const props = defineProps({
  data: Array,
  sortKey: String,
  sortOrder: Number,
  page: Number,
})

const emit = defineEmits(['delete-record', 'sort']);

const clickCounts = ref({});

const handleDelete = (index) => {
  emit('delete-record', index + 5*(props.page-1));
};

const handleSort = (key) => {
  const currentCount = clickCounts.value[key] || 0;
  clickCounts.value[key] = (currentCount + 1) % 3;

  if (clickCounts.value[key] === 0) {
    emit('sort', { key: '', order: 1 });
  } else {
    emit('sort', { key, order: clickCounts.value[key] === 1 ? 1 : -1 });
  }
};
</script>

<template>
  <div id="table">
    <div id="table-header">
      <div class="col-container">
        <div
            @click="handleSort('CompanyName')"
            class="row-header"
        >
          Название
          <span v-if="sortKey === 'CompanyName' && sortOrder === 1" >↑</span>
          <span v-else-if="sortKey === 'CompanyName' && sortOrder === -1" >↓</span>
        </div>
        <div
            @click="handleSort('DirectorName')"
            class="row-header"
        >
          ФИО директора
          <span v-if="sortKey === 'DirectorName' && sortOrder === 1" >↑</span>
          <span v-else-if="sortKey === 'DirectorName' && sortOrder === -1" >↓</span>
        </div>
        <div class="row-header">Номер телефона</div>
        <div class="row-header"></div>
      </div>
    </div>
    <div id="table-body">
      <div class="col-container" v-for="(record, index) in props.data" :key="index">
        <div class="row">{{ record.CompanyName }}</div>
        <div class="row">{{ record.DirectorName }}</div>
        <div class="row">{{ record.PhoneNumber }}</div>
        <button-component msgProps="X" type="delete" @click="handleDelete(index)"/>
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