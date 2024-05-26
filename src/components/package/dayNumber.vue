<script setup lang="ts">
const props = withDefaults(defineProps<{
  dayLists: Array<{
    id: number
    day: number
    type: number
  }>
  nowDay: number
  // homeWordListLength: number
}>(), {
  dayLists: () => [],
})
const emit = defineEmits(['homeWorkList'])
const curDay = ref(props.nowDay)
const nowIndex = ref()
const index = ref('')

watchEffect(() => {
  // 监听 props.nowDay 的变化,并更新副本
  curDay.value = props.nowDay
  nowIndex.value = props.nowDay
  // index.value = `id${props.nowDay}`
})
// 点击天，tab切换作业
function clickTab(index: number) {
  curDay.value = index
  if (nowIndex.value !== index) {
    nowIndex.value = index
    emit('homeWorkList', index)
  }
}
setTimeout(() => {
  index.value = `id${curDay.value}`
}, 500)
</script>

<template>
  <view>
    <scroll-view class="w-100% whitespace-nowrap" scroll-x="true" :scroll-into-view="index" :show-scrollbar="false">
      <view v-for="(item, indexed) in props.dayLists" :id="`id${item.id}`" :key="item.id" class="ml-40rpx inline-flex flex-col items-start">
        <view class="mt-77rpx rounded-20rpx flex-center h-66rpx w-66rpx" :class="[curDay === indexed ? 'bg-$background-color c-[#FFFFFF]' : '']" @click="clickTab(indexed)">
          <text class="mt-21rpx text-36rpx relative top-[-15%]">
            {{ item.day }}
          </text>
        </view>
        <view v-if="item.type === 0" class="mt-15rpx bg-$background-color rounded-50% relative h-12rpx w-12rpx left-36%" />
        <view v-else class="mt-15rpx relative h-34rpx" />
      </view>
    </scroll-view>
  </view>
</template>

<style>
</style>
