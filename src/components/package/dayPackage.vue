<script setup lang="ts">
const emit = defineEmits(['getDay', 'nowMonth'])
const date = ref('')
const nowDay = ref()
const classList = ref(0)
const array = ['全部班级', '一年级', '二年级', '三年级']
// 更新年月
function bindDateChange(e: any) {
  date.value = e.detail.value.split('-').join('/')
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
  const day = date.getDate()
  nowDay.value = day - 1
  emit('nowMonth', year, month, day)
  if (type === 'start')
    year = year - 60
  else if (type === 'end')
    year = year + 2

  month = month > 9 ? month : `0${month}`
  return `${year}/${month}`
}

onMounted(() => {
  const currentDate = getDate({ format: false })
  date.value = currentDate
})
</script>

<template>
  <view class="between text-38rpx h-70rpx items-center">
    <view>
      <view class="inline-block">
        <picker mode="date" :value="date" :start="startDate" :end="endDate" fields="month" @change="bindDateChange">
          <view class="uni-input font-600 c-$text-color-0">
            {{ date }}
          </view>
        </picker>
      </view>
      <view class="i-carbon-chevron-down ml-17rpx inline-block font-600 c-$icon-color-1" />
    </view>

    <!-- 班级 -->
    <view class="between p-15rpx mr-30rpx b-1rpx b-$base-color rounded-25rpx b-solid text-26rpx inline-flex h-70rpx w-250rpx">
      <view class="inline-block">
        <picker :value="classList" :range="array" @change="bindClassChange">
          <view class="uni-input">
            {{ array[classList] }}
          </view>
        </picker>
      </view>
      <view class="i-carbon-chevron-down inline-block c-$icon-color-1" />
    </view>
  </view>
</template>

<style>

</style>
