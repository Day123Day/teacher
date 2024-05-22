<script setup lang="ts">
const emit = defineEmits(['getDay'])
const date = ref('')
const classList = ref(0)
const array = ['全部班级', '一年级', '二年级', '三年级']
// 更新数据
function bindDateChange(e: any) {
  date.value = e.detail.value
  emit('getDay', date.value)
}
// 班级更新
function bindClassChange(e: any) {
  classList.value = e.detail.value
}
const startDate = computed(() => {
  return getDate('start')
})
const endDate = computed(() => {
  return getDate('end')
})
// 获得日期
function getDate(type: any) {
  const date = new Date()
  let year = date.getFullYear()
  let month: any = date.getMonth() + 1

  if (type === 'start')
    year = year - 60
  else if (type === 'end')
    year = year + 2

  month = month > 9 ? month : `0${month}`
  return `${year} / ${month}`
}

onMounted(() => {
  const currentDate = getDate({ format: true })
  date.value = currentDate
})
</script>

<template>
  <view class="text-38rpx flex h-70rpx justify-between items-center">
    <view>
      <view class="uni-list inline-block">
        <picker mode="date" :value="date" :start="startDate" :end="endDate" fields="month" @change="bindDateChange">
          <view class="uni-input">
            {{ date }}
          </view>
        </picker>
      </view>
      <view class="i-carbon-chevron-down ml-17rpx inline-block" />
    </view>

    <!-- 班级 -->
    <view class="p-20rpx mr-30rpx inline-block b-1rpx b-$base-color rounded-25rpx b-solid text-26rpx h-70rpx w-250rpx float-right" @change="bindClassChange">
      <view class="uni-list-cell-db inline-block">
        <picker :value="classList" :range="array" @change="bindClassChange">
          <view class="uni-input">
            {{ array[classList] }}
          </view>
        </picker>
      </view>
      <view class="i-carbon-chevron-down ml-70rpx inline-block" />
    </view>
  </view>
</template>

<style>

</style>
