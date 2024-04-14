<template>
  <div class="wrapper">
    <a-tree
      :data="orgData"
      :field-names="{
        'key': 'id',
        'title': 'name'
      }" 
      :load-more="loadMore"
      @select="select"
    />
  </div>
</template>
  
<script setup>
import { ref, onMounted } from 'vue'
import orgApi from '../api/org'

const emit = defineEmits(["selectOrg"]);

const orgData = ref([])

// 动态加载子节点
const loadMore = (nodeData) => {
  return new Promise((resolve) => {
    orgApi.query(nodeData.id).then((user) => {
      nodeData.children = user
        resolve()
    }) 
  });
};

// 选择节点
const select = (data) => {
  emit('selectOrg', data[0])
}

onMounted(() => {
  orgApi.query().then((user) => {
    orgData.value = user
    emit('selectOrg', orgData.value[0].id)
  })
  
});
</script>
  
<style scoped>
.wrapper {
  width: 200px;
  height: 600px;
  overflow: auto;
}
</style>