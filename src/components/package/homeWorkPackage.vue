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
function condition(type: number) {
  const condition = {
    OK: {
      type: '已批改',
    },
    NO: {
      type: '未批改',
    },
    OR: {
      type: '批改中',
    },
  }
  if (type === 0)
    return condition.OK.type

  else if (type === 1)
    return condition.NO.type

  else
    return condition.OR.type
}
function icon(type: number) {
  const condition = {
    OK: {
      icon: 'i-carbon-checkmark',
    },
    NO: {
      icon: 'i-carbon-help-filled',
    },
    OR: {
      icon: 'i-carbon-hourglass',
    },
  }
  if (type === 0)
    return condition.OK.icon

  else if (type === 1)
    return condition.NO.icon

  else
    return condition.OR.icon
}
function color(type: number) {
  const condition = {
    OK: {
      icon: 'color:#01A76F',
    },
    NO: {
      icon: 'color:#FFC281',
    },
    OR: {
      icon: 'color:#8CA0C6',
    },
  }
  if (type === 0)
    return condition.OK.icon

  else if (type === 1)
    return condition.NO.icon

  else
    return condition.OR.icon
}
</script>

<template>
  <view>
    <view v-if="props.homeWordLists.length">
      <view v-for="(item, id) in props.homeWordLists" :key="id" class="px-25rpx pt-30rpx mb-30rpx bg-$base-color rounded-10rpx h-290rpx w-690rpx" model="props.homeWordList" :value="props.homeWordLists">
        <!-- 第一行 -->
        <view class="between h-40rpx">
          <view class="flex items-center">
            <view class="bg-$background-color-0 rounded-20rpx flex-center inline-flex h-40rpx w-80rpx">
              <text class="text-20rpx text-center c-$text-color-4">
                基础
              </text>
            </view>
            <view class="ml-20rpx inline-block text-30rpx font-600 c-$text-color-0">
              {{ item.course }}
            </view>
          </view>
          <!-- 批该状态 -->
          <view class="inline-flex items-center">
            <view class="mr-13rpx inline-block c-$background-color h-24rpx w-24rpx" :class="icon(item.type)" :style="color(item.type)" />
            <text class="text-22rpx c-$text-color-0">
              {{ condition(item.type) }}
            </text>
          </view>
        </view>
        <!-- 第二行 -->
        <view class="mt-30rpx text-24rpx between">
          <view class="inline-block">
            <text class="c-$text-color-0">
              发布日期：
            </text>
            <text class="c-$oborder-color">
              {{ item.start }}
            </text>
          </view>
          <view class="inline-block">
            <text class="c-$text-color-0">
              结束批改：
            </text>
            <text class="c-$oborder-color">
              {{ item.end }}
            </text>
          </view>
        </view>
        <!-- 第三行 -->
        <view class="mb-30rpx mt-60rpx between">
          <view class="inline-block">
            <view class="mb-10rpx text-36rpx">
              <text class="c-$background-color">
                {{ item.correct }}
              </text>
              <text>/{{ item.total }}</text>
            </view>
            <view class="text-22rpx c-$text-color-0">
              <text>以批改人数</text>
            </view>
          </view>
          <view class="flex items-center">
            <view class="b-1rpx b-$border-color-2 rounded-33rpx b-solid flex-center inline-flex h-66rpx w-170rpx">
              <text class="text-26rpx text-center c-$text-color-0">
                作业详情
              </text>
            </view>
            <view class="ml-20rpx inline-block bg-$background-color rounded-33rpx flex flex-center h-66rpx w-170rpx">
              <text class="text-26rpx text-center color-$base-color">
                学情报告
              </text>
            </view>
          </view>
        </view>
      </view>
    </view>
    <view v-else class="h-450rpx">
      <guodu-empty />
    </view>
  </view>
</template>

<style>

</style>
