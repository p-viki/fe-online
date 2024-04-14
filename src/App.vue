<template>
  <a-tabs default-active-key="1">
    <a-tab-pane key="1" title="成员管理">
      <div class="flex">
        <org-tree @selectOrg="selectOrg"></org-tree>
        <user-table :orgId="orgId"></user-table>
      </div>
    </a-tab-pane>
    <a-tab-pane key="2" title="团队管理">
    </a-tab-pane>
    <a-tab-pane key="3" title="职位维护">
    </a-tab-pane>
  </a-tabs>
</template>
  
<script setup>
import {ref} from 'vue'
import OrgTree from './components/OrgTree.vue'
import UserTable from './components/UserTable.vue'

const orgId = ref('')

const selectOrg = (id) => {
  orgId.value = id
}
</script>

<style>
  
</style>