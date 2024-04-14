<template>
  <div class="wrapper">
    <a-input-search :style="{width:'320px', marginBottom: '10px'}" placeholder="搜索" v-model="keyword"/>
    <a-table :data="computedTableData" >
      <template #columns>
        <a-table-column title="序号" width="80">
          <template #cell="{rowIndex}">
            {{ rowIndex + 1 }}
          </template>
        </a-table-column>
        <a-table-column title="姓名" data-index="name" :sortable="{sortDirections: ['ascend', 'descend']}"></a-table-column>
      </template>
    </a-table>
  </div>
</template>
  
<script setup>
import { ref, watch, defineProps, computed,onMounted } from 'vue'
import userApi from '../api/user'

const props = defineProps({
  orgId: String, 
});

watch(() => props.orgId, (nv) => {
    userApi.query({orgId: nv}).then((user) => {
    tableData.value = user
  })
})

const keyword = ref('')
const tableData = ref([])

// 关键词筛选数组
const computedTableData = computed(() => {
  const filteredArray = tableData.value.filter(item => item.name.includes(keyword.value));
  return filteredArray
})

onMounted(() => {
  userApi.query({orgId: props.orgId}).then((user) => {
    tableData.value = user
  })
});
</script>
  
<style scoped>
.wrapper {
  padding: 0 20px;
  width: 100%;
}
  
</style>