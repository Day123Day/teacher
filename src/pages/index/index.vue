<script setup lang="ts">
import { Fetch } from '~/utils/fetch'
import { api } from '~/config/api'

const dayList = ref<Array<{
  id: number
  day: number
  type: number
}>>([])
const nowDay = ref(1)
const nowIndex = ref()
const days = ref()
const homeWordListLength = ref()
const homeWordLists = ref<Array<{
  id: number
  course: string
  type: number
  start: string
  end: string
  total: number
  correct: number
}>>([])
// 监听下拉刷新
onPullDownRefresh(() => {
  setTimeout(() => {
    uni.stopPullDownRefresh()
  }, 1000)
})
// 计算对应月的天数
function getDaysInMonth(year: number, month: number) {
  return new Date(year, month, 0).getDate()
}
// 改变月得到该月对应的天数
function getDay(day: string) {
  const [year, month] = day.split('/').map(Number)
  const dayNumber = getDaysInMonth(year, month)
  days.value = dayNumber
  dayNumberQuer(dayNumber)
  setTimeout(() => {
    homeWorkList(nowIndex.value)
  }, 100)
  // console.log('111', nowIndex.value)
}
// 获得后台返回天数的数组
function dayNumberQuer(dayNumber: number) {
  Fetch(api.getDay, { data: { dayNumber }, method: 'POST' }).then((res) => {
    dayList.value = res
  })
}
// 获得后台返回作业量的数组
function homeWorkQuer() {
  Fetch(api.getHomeWordList, { method: 'GET' }).then((res) => {
    homeWordLists.value = res
    // homeWordListLength.value = homeWordLists.value.length
    // console.log(homeWordListLength.value)
  })
}
// 获得作业
function homeWorkList(index: number) {
  nowIndex.value = index

  if (dayList.value[index].type === 0)
    homeWorkQuer()

  else
    homeWordLists.value = []
}
// 获得当前月的天数
function nowMonth(year: number, month: number, day: number) {
  const dayNumber = getDaysInMonth(year, month)
  dayNumberQuer(dayNumber)
  nowDay.value = day - 1
}
// 获得当前天的作业
function nowHomeWork() {
  if (dayList.value[nowDay.value].type === 0)
    homeWorkQuer()

  else
    homeWordLists.value = []
}
// 刚开始就改变年月分
// function selectedDay(selectedDay: number) {
//   setTimeout(() => {
//     console.log(days.value)
//   }, 3000)
// console.log(selectedDay)
// }
// 等待一秒后得到今天的作业
setTimeout(() => {
  nowHomeWork()
}, 1000)
</script>

<template>
  <view class="bg-[url(../static/images/23.png)] bg-contain bg-no-repeat px-30rpx bg-$body-background-color">
    <view class="pt-48rpx mb-54rpx text-40rpx font-600 c-$text-color-0">
      <text>
        智慧作业教师端
      </text>
    </view>
    <!-- 日期年月 -->
    <day-package @get-day="getDay" @now-month="nowMonth" />
    <!-- 日期天数 -->
    <day-number :day-lists="dayList" :now-day="nowDay" :home-word-list-length="homeWordListLength" @home-work-list="homeWorkList" />

    <!-- 作业功能 -->
    <homeWorkAbility />
    <!-- 作业组件 -->
    <homeWorkPackage :home-word-lists="homeWordLists" />
  </view>
</template>

<style lang="less" scoped>
</style>
