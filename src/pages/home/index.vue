<script lang="ts" setup>
import { ref } from 'vue'

definePage({
  type: 'home',
  style: {
    navigationBarTitleText: '首页',
  },
})
/**
 * 跳转至通行证页面
 */
function navigateToPass() {
  uni.switchTab({ url: '/pages/pass/index' })
}
function navigateToAppointment() {
  console.log('跳转预约页面')
}
function navigateToVerify() {
  console.log('跳转核销页面')
}

const current = ref(0)

const swiperList = ref([
  'https://wot-ui.cn/assets/redpanda.jpg',
  'https://wot-ui.cn/assets/capybara.jpg',
  'https://wot-ui.cn/assets/panda.jpg',
  'https://wot-ui.cn/assets/moon.jpg',
  'https://wot-ui.cn/assets/meng.jpg',
])
</script>

<template>
  <view class="page">
    <!-- 首页轮播图 -->
    <wd-swiper v-model:current="current" :list="swiperList" autoplay :indicator="{ type: 'dots' }" class="mb-[24rpx]" />
    <view class="px-[24rpx]">
      <!-- 有效通行证提示 -->
      <view class="mb-[24rpx] flex-1 border-2 border-[#b7eb8f] rounded-[16rpx] border-solid bg-[#f6ffed]" @click="navigateToPass">
        <view class="flex items-center gap-[24rpx] p-[32rpx_28rpx]">
          <view>
            <view class="i-carbon-security text-[48rpx] text-green-500" />
          </view>
          <view class="flex-1">
            <text class="mb-[4rpx] block text-[28rpx] text-[#333] font-600">
              您有1张有效通行证
            </text>
            <text class="block text-[24rpx] text-[#52c41a]">
              剩余 02:03:55 失效，请及时使用
            </text>
          </view>
          <view class="i-carbon-chevron-right text-gray-300" />
        </view>
      </view>

      <!-- 预约入口 -->
      <view>
        <view class="flex gap-[24rpx]">
          <view class="mb-[24rpx] flex-1 border-2 border-blue-300 rounded-[16rpx] border-solid bg-[#fff]">
            <view class="flex flex-col gap-[12rpx] p-[32rpx_28rpx]">
              <view class="i-carbon-task-add text-[60rpx] text-blue-500" />
              <text class="mb-[6rpx] block text-[36rpx] text-[#333] font-600">访客预约</text>
              <text class="block text-[24rpx] text-[#999]">访客入园预约</text>
            </view>
          </view>
          <view class="mb-[24rpx] flex-1 border-2 border-orange-300 rounded-[16rpx] border-solid bg-[#fff]">
            <view class="flex flex-col gap-[12rpx] p-[32rpx_28rpx]">
              <view class="i-carbon-delivery-truck text-[60rpx] text-orange-500" />
              <text class="mb-[6rpx] block text-[36rpx] text-[#333] font-600">货车预约</text>
              <text class="block text-[24rpx] text-[#999]">车辆入园预约</text>
            </view>
          </view>
        </view>
        <view>
          <!-- 扫描核销卡片--需要分配核销权限 -->
          <view class="mb-[24rpx] flex-1 border-2 border-rose-300 rounded-[16rpx] border-solid bg-[#fff]" @click="navigateToVerify">
            <view class="flex items-center gap-[24rpx] p-[32rpx_28rpx]">
              <view>
                <view class="i-carbon-scan-alt text-[60rpx] text-rose-500" />
              </view>
              <view class="flex-1">
                <text class="mb-[6rpx] block text-[36rpx] text-[#333] font-600">
                  扫码核销
                </text>
                <text class="block text-[24rpx] text-[#999]">
                  门卫扫描通行证进行核销确认
                </text>
              </view>
              <view class="i-carbon-chevron-right text-gray-300" />
            </view>
          </view>

          <!-- 菜单导航栏 -->
          <view class="mb-[24rpx] rounded-[16rpx] bg-[#fff]">
            <view class="flex items-center gap-[24rpx] p-[32rpx_28rpx]">
              <view class="menu-item">
                <view class="menu-item__icon">
                  <view class="i-carbon-calendar-add text-blue-500" />
                </view>
                <text class="menu-item__label">现场预约</text>
              </view>
              <view class="menu-item">
                <view class="menu-item__icon">
                  <view class="i-carbon-document text-blue-500" />
                </view>
                <text class="menu-item__label">预约记录</text>
              </view>
              <view class="menu-item">
                <view class="menu-item__icon">
                  <view class="i-carbon-help text-blue-500" />
                </view>
                <text class="menu-item__label">使用帮助</text>
              </view>
            </view>
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<style scoped lang="scss">
.menu-item {
  flex: 1;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 12rpx;

  &__icon {
    width: 80rpx;
    height: 80rpx;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 16rpx;
    background: #eff6ff;
    font-size: 40rpx;
  }

  &__label {
    font-size: 24rpx;
    color: #666;
  }
}
</style>
