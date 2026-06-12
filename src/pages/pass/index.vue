<script lang="ts" setup>
import QrCode from '@/components/QrCode.vue'
import { onMounted, ref } from 'vue'

definePage({
  style: {
    navigationBarTitleText: '通行证',
    navigationBarBackgroundColor: '#1890FF',
    navigationBarTextStyle: 'white',
  },
})

const qrCodeContent = ref('52352352fewa532532')
const leaveTime = ref('') // 后端返回的离开时间，如 "2026-06-10 12:00"
const remainder = ref(0)

/** 获取指定日期到当日 24:00:00 的剩余毫秒数 */
function getRemainderToMidnight(date: Date): number {
  console.log(date)
  const endOfDay = new Date(date.getFullYear(), date.getMonth(), date.getDate() + 1, 0, 0, 0)
  return endOfDay.getTime() - Date.now()
}

onMounted(() => {
  leaveTime.value = '2026-06-10 12:00'
  remainder.value = getRemainderToMidnight(new Date(leaveTime.value))
})
</script>

<template>
  <view class="page p-[24rpx]">
    <view class="rounded-[16rpx] bg-[#fff] p-[32rpx]">
      <view class="mb-[36rpx] flex justify-center">
        <text class="text-[36rpx] font-600">访客二维码</text>
      </view>
      <view class="mb-[32rpx] flex justify-center">
        <QrCode :data="qrCodeContent" :size="300" :cell-size="13" />
      </view>
      <view class="mb-[24rpx] text-center">
        <text class="mb-[8rpx] block text-[#666] font-[26rpx]">剩余有效时间 </text>
        <wd-count-down :time="remainder" custom-class="block font-700" custom-style="--wot-count-down-font-size: 56rpx" />
      </view>
    </view>
  </view>
</template>
