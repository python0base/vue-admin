<template>
  <div class="user">
    <!-- 1.搜索区域 -->
    <Pagesearch @query-click="handleQueryClick" @reset-click="handleResetClick" />

    <!-- 2.展示区域 -->
    <Pagecontent
      ref="contentRef"
      @new-data-click="handleNewDataClick"
      @edit-data-click="handleEditDataClick"
    />

    <!-- 3.新建和编辑 -->
    <Pagemodal ref="modalRef" />
  </div>
</template>

<script setup lang="ts" name="user">
import Pagesearch from './c-cpns/page-search.vue'
import Pagecontent from './c-cpns/page-content.vue'
import Pagemodal from './c-cpns/page-modal.vue'
import { ref } from 'vue'

// 1.重置功能
const contentRef = ref<InstanceType<typeof Pagecontent>>()
function handleQueryClick(searchInfo: any) {
  contentRef.value?.fetchUserListData(searchInfo)
}
function handleResetClick() {
  contentRef.value?.handleResetClick()
}

// 2.新建和编辑数据
const modalRef = ref<InstanceType<typeof Pagemodal>>()
function handleNewDataClick() {
  modalRef.value?.setDialogVisible()
}
function handleEditDataClick(data: any) {
  modalRef.value?.setDialogVisible(false, data)
}
</script>

<style lang="less" scoped></style>
