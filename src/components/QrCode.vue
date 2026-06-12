<script lang="ts" setup>
import UQRCode from 'uqrcodejs'
import { computed, onMounted, ref, watch } from 'vue'

const props = withDefaults(defineProps<{
  /** 二维码承载的数据 */
  data: string
  /** 二维码整体尺寸（单位：px），默认 300 */
  size?: number
  /** 每个模块的尺寸（单位：rpx），默认 13 */
  cellSize?: number
}>(), {
  size: 300,
  cellSize: 13,
})

const modules = ref<any[][]>([])

const cellStyle = computed(() => ({
  width: `${props.cellSize}rpx`,
  height: `${props.cellSize}rpx`,
}))

function generate() {
  const qr = new UQRCode()
  qr.data = props.data
  qr.size = props.size
  qr.make()
  modules.value = qr.modules
}

onMounted(() => generate())
watch(() => props.data, generate)
</script>

<template>
  <view class="qr-code">
    <view v-for="(row, rowI) in modules" :key="rowI" class="flex flex-row">
      <view
        v-for="(col, colI) in row"
        :key="colI"
        :class="col.isBlack ? 'bg-[#000]' : 'bg-[#fff]'"
        :style="cellStyle"
      />
    </view>
  </view>
</template>
