<script setup>
import { ref, computed } from 'vue';
import data from '/src/data.json';
import TableComponent from "@/components/TableComponent.vue";
import ButtonComponent from "@/components/UI/ButtonComponent.vue";
import InputComponent from "@/components/UI/InputComponent.vue";
import DialogComponent from "@/components/DialogComponent.vue";

const itemsPerPage = 5;
const currentPage = ref(1);

const sortKey = ref('');
const sortOrder = ref(1);

const loadData = () => {
  const savedData = localStorage.getItem('data');
  return savedData?JSON.parse(savedData):data;
};

const saveData = (data) => {
  localStorage.setItem('data', JSON.stringify(data));
};

const filter = ref('');
const showDialog = ref(false);
const tableData = ref(loadData());

const sortedAndFilteredData = computed(() => {
  let filteredData = tableData.value.filter(item =>
      item.DirectorName.toLowerCase().includes(filter.value.toLowerCase())
  );

  if (sortKey.value) {
    filteredData.sort((a, b) => {
      const valueA = a[sortKey.value].toLowerCase();
      const valueB = b[sortKey.value].toLowerCase();

      if (valueA < valueB) return -1 * sortOrder.value;
      if (valueA > valueB) return 1 * sortOrder.value;
      return 0;
    });
  }

  return filteredData;
});

const paginatedData = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage;
  const end = start + itemsPerPage;
  return sortedAndFilteredData.value.slice(start, end);
});

const totalPages = computed(() => Math.ceil(sortedAndFilteredData.value.length / itemsPerPage));

const changePage = (page) => {
  if (page >= 1 && page <= totalPages.value) {
    currentPage.value = page;
  }
};

const handleSort = ({ key, order }) => {
  sortKey.value = key;
  sortOrder.value = order;
};

const addRecord = (record) => {
  tableData.value.push(record);
  saveData(tableData.value);
};

const deleteRecord = (index) => {
  tableData.value.splice(index, 1);
  saveData(tableData.value);
};
</script>

<template>
  <dialog-component
      :showDialog="showDialog"
      @update:showDialog="showDialog = $event"
      @add-record="addRecord"
  />
  <div id="content">
    <div id="header">
      <input-component
          labelInput="filter"
          placeholderInput="Найти по ФИО..."
          v-model="filter"
      />
      <button-component
          msgProps="Добавить"
          type="add"
          @click="showDialog = true"
      />
    </div>
    <table-component
        :data="paginatedData"
        :sortKey="sortKey"
        :sortOrder="sortOrder"
        :page="currentPage"
        @delete-record="deleteRecord"
        @sort="handleSort"
    />
    <div style="margin-top: 20px">
      <button-component
          @click="changePage(currentPage - 1)"
          :check="!(currentPage === 1)"
          msgProps="Предыдущая"
          type="pagination"
      />
      <slot>{{ currentPage }} / {{ totalPages }}</slot>
      <button-component
          @click="changePage(currentPage + 1)"
          :check="!(currentPage === totalPages)"
          msgProps="Следующая"
          type="pagination"
      />
    </div>
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
