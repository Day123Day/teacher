<script setup lang="ts">
const props = withDefaults(defineProps<{
  dayLists: Array<{
    id: number
    day: number
    type: number
  }>
  nowDay: number
}>(), {
  dayLists: () => [],
})
const emit = defineEmits(['homeWorkList'])
const curDay = ref(props.nowDay)
const old = ref({
  scrollTop: 0,
})

function scroll(e: any) {
  old.value.scrollTop = e.detail.scrollTop
}

// 点击天，tab切换作业
function clickTab(index: number) {
  emit('homeWorkList', index)
}
</script>

<template>
  <view>
    <scroll-view class="whitespace-nowrap" scroll-x="true" :show-scrollbar="false" @scroll="scroll">
      <view v-for="(item, index) in props.dayLists" :key="item.id" class="ml-40rpx inline-flex flex-col items-start">
        <view class="mt-77rpx rounded-20rpx flex-center h-66rpx w-66rpx" :style="[curDay === index ? 'backgroundColor:#00A76E;color:#FFFFFF' : '']" @tap="curDay = index" @click="clickTab(index)">
          <text class="mt-21rpx text-36rpx relative top-[-15%]">
            {{ item.day }}
          </text>
        </view>
        <view v-if="item.type === 0" class="mt-15rpx text-22rpx relative left-[-10%]">
          三份作业
        </view>
        <view v-else class="mt-15rpx relative h-34rpx" />
      </view>
    </scroll-view>
  </view>
</template>

<style>
</style>
