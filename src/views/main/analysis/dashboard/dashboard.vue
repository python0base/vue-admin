<template>
  <div class="dashboard">
    <el-row :gutter="10">
      <el-col :span="12">
        <hy-card title="分类商品数量(饼图)">
          <pie-echart :pieData="categoryGoodsCount"></pie-echart>
        </hy-card>
      </el-col>
      <!-- <el-col :span="10">
        <hy-card title="不同城市商品销量">
          <map-echart :mapData="addressGoodsSale"></map-echart>
        </hy-card>
      </el-col> -->
      <el-col :span="12">
        <hy-card title="分类商品数量(玫瑰图)">
          <rose-echart :roseData="categoryGoodsCount"></rose-echart>
        </hy-card>
      </el-col>
    </el-row>

    <el-row :gutter="10" class="row">
      <el-col :span="12">
        <hy-card title="分类商品的销量">
          <line-echart :labels="categoryGoodsSale.labels" :values="categoryGoodsSale.values" />
        </hy-card>
      </el-col>
      <el-col :span="12">
        <hy-card title="分类商品的收藏">
          <bar-echart :labels="categoryGoodsSale.labels" :values="categoryGoodsSale.values" />
        </hy-card>
      </el-col>
    </el-row>
  </div>
</template>

<script setup lang="ts" name="dashboard">
import { computed } from 'vue'
import useAnalysisStore from '@/store/main/analysis/analyisis'
import HyCard from '@/base-ui/card/card.vue'
import {
  PieEchart,
  MapEchart,
  RoseEchart,
  BarEchart,
  LineEchart
} from '@/components/page-charts/index'

const analysisStore = useAnalysisStore()
analysisStore.fetchAnalysisDataAction()

const categoryGoodsCount = computed(() => {
  return analysisStore.categoryGoodsCount.map((item: any) => {
    return { value: item.goodsCount, name: item.name }
  })
})
const goodsSaleTop10 = computed(() => {
  return analysisStore.goodsSaleTop10.map((item: any) => {
    return { value: item.saleCount, name: item.name }
  })
})
const categoryGoodsSale = computed(() => {
  const goodsSale = analysisStore.categoryGoodsSale
  const labels: string[] = []
  const values: any[] = []
  for (const item of goodsSale) {
    labels.push(item.name)
    values.push(item.goodsCount)
  }
  return { labels, values }
})
const addressGoodsSale = computed(() => {
  return analysisStore.goodsAddressSale.map((item: any) => {
    return { name: item.address, value: item.count }
  })
})
</script>

<style scoped lang="less">
.dashboard {
  background-color: #f5f5f5;
  .row {
    margin-top: 20px;
  }
}
</style>
