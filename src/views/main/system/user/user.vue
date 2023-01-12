<template>
  <div class="user">
    <!-- 1.搜索区域 -->
    <Page1Search @query-click="handleQueryClick" @reset-click="handleResetClick" />

    <!-- 2.展示区域 -->
    <Page1Content
      ref="contentRef"
      @new-data-click="handleNewDataClick"
      @edit-data-click="handleEditDataClick"
    />

    <!-- 3.新建和编辑 -->
    <Page1Modal ref="modalRef" />
  </div>
</template>

<script setup lang="ts" name="user">
import Page1Search from './c-cpns/page1-search.vue'
import Page1Content from './c-cpns/page1-content.vue'
import Page1Modal from './c-cpns/page1-modal.vue'
import { ref } from 'vue'

// 1.重置功能
const contentRef = ref<InstanceType<typeof Page1Content>>()
function handleQueryClick(searchInfo: any) {
  contentRef.value?.fetchUserListData(searchInfo)
}
function handleResetClick() {
  contentRef.value?.handleResetClick()
}

// 2.新建和编辑数据
const modalRef = ref<InstanceType<typeof Page1Modal>>()
function handleNewDataClick() {
  modalRef.value?.setDialogVisible()
}
function handleEditDataClick(data: any) {
  modalRef.value?.setDialogVisible(false, data)
}
</script>

<style lang="less" scoped></style>
