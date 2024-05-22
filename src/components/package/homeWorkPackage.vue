<script setup lang="ts">
const props = withDefaults(defineProps<{
  homeWordLists: Array<{
    id: number
    course: string
    type: number
    start: string
    end: string
    total: number
    correct: number
  }>
}>(), {
  homeWordLists: () => [],
})
</script>

<template>
  <view>
    <view v-for="(item, id) in props.homeWordLists" :key="id" class="px-25rpx pt-30rpx mb-30rpx bg-[#FFFFFF] rounded-10rpx h-290rpx w-690rpx" model="props.homeWordList" :value="props.homeWordLists">
      <!-- 第一行 -->
      <view class="flex h-40rpx w-690rpx items-center">
        <view class="bg-[#EBF6FF] rounded-20rpx flex-center h-40rpx w-80rpx">
          <text class="text-20rpx text-center color-[#0084FF]">
            基础
          </text>
        </view>
        <view class="ml-20rpx text-30rpx font-600">
          {{ item.course }}
        </view>
        <view class="ml-222rpx inline-block">
          <!-- 批该 -->
          <view v-if="item.type === 1">
            <view class="i-carbon-checkmark mr-13rpx inline-block b-1rpx b-[#8F9AA8] b-dotted c-[#00A76E] h-24rpx w-24rpx" />
            <text class="text-22rpx">
              已批该
            </text>
          </view>
          <!-- 批改中 -->
          <view v-else-if="item.type === 0" class="flex h-24rpx items-center">
            <view class="i-carbon-rule-test mr-13rpx inline-block b-1rpx b-[#8F9AA8] b-dotted h-24rpx w-24rpx" />
            <text class="text-22rpx">
              批该中
            </text>
          </view>
          <!-- 未批该 -->
          <view v-else>
            <view class="i-carbon-rule-cancelled mr-13rpx inline-block b-1rpx b-[#8F9AA8] b-dotted h-24rpx w-24rpx" />
            <text class="text-22rpx">
              未批改
            </text>
          </view>
        </view>
      </view>
      <!-- 第二行 -->
      <view class="mt-30rpx text-24rpx flex justify-between">
        <view class="inline-block">
          <text>发布日期：</text>
          <text class="c-[#8F9AA8]">
            {{ item.start }}
          </text>
        </view>
        <view class="inline-block">
          <text>结束批改：</text>
          <text class="c-[#8F9AA8]">
            {{ item.end }}
          </text>
        </view>
      </view>
      <!-- 第三行 -->
      <view class="mb-30rpx mt-60rpx flex justify-between">
        <view class="inline-block">
          <view class="mb-10rpx text-36rpx">
            <text class="c-[#00A76E]">
              {{ item.correct }}
            </text>
            <text>/{{ item.total }}</text>
          </view>
          <view class="text-22rpx">
            <text>以批改人数</text>
          </view>
        </view>
        <view class="flex items-center">
          <view class="inline-block b-1rpx b-[#C9CED9] rounded-33rpx b-solid flex flex-center h-66rpx w-170rpx">
            <text class="text-26rpx text-center">
              作业详情
            </text>
          </view>
          <view class="ml-20rpx inline-block bg-[#00A76E] rounded-33rpx flex flex-center h-66rpx w-170rpx">
            <text class="text-26rpx text-center color-[#FFFFFF]">
              学情报告
            </text>
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<style>

</style>
