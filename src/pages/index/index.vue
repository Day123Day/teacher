<script setup lang="ts">
import { ref } from 'vue'
import { Fetch } from '~/utils/fetch'

const date = ref('')
const dayList: any = ref([])
const curDay = ref(0)
const homeWordList: any = ref([])
const classList = ref(0)
const array = ['全部班级', '一年级', '二年级', '三年级']

// 更新数据
function bindDateChange(e: any) {
  date.value = e.detail.value
}
// 班级更新
function bindClassChange(e: any) {
  classList.value = e.detail.value
  // console.log(1111)
}
// tab切换
function clickTab(index: any) {
  // console.log(item.day)
  // Fetch('http://127.0.0.1:8081/api/day', { data: { day: item.day }, method: 'POST' })

  if (index === 1) {
    homeWordList.value = null
  }
  else {
    Fetch('http://127.0.0.1:8081/api/test', { method: 'GET' }).then((res) => {
      homeWordList.value = res
    })
  }
}
// 获得日期
function getDate(type: any) {
  const date = new Date()
  let year = date.getFullYear()
  let month: any = date.getMonth() + 1
  // let day = date.getDate()

  if (type === 'start')
    year = year - 60
  else if (type === 'end')
    year = year + 2

  month = month > 9 ? month : `0${month}`
  // day = day > 9 ? day : `0${day}`
  return `${year}-${month}`
  // return `${year}-${month}-${day}`
}

const startDate = computed(() => {
  return getDate('start')
})
const endDate = computed(() => {
  return getDate('end')
})

onMounted(() => {
  const currentDate = getDate({ format: true })
  date.value = currentDate
})

Fetch('http://127.0.0.1:8081/api/dayList', { method: 'GET' }).then((res) => {
  dayList.value = res
})
Fetch('http://127.0.0.1:8081/api/test', { method: 'GET' }).then((res) => {
  homeWordList.value = res
})
</script>

<template>
  <view class="bg-[url(../static/images/23.png)] px-30rpx bg-[#F5F5F9]">
    <view class="pt-48rpx mb-54rpx text-40rpx">
      <text>
        智慧作业教师端
      </text>
    </view>
    <!-- 日期年月 -->
    <view class="text-38rpx">
      <view class="uni-list inline-block">
        <picker mode="date" :value="date" :start="startDate" :end="endDate" fields="month" @change="bindDateChange">
          <view class="uni-input">
            {{ date }}
          </view>
        </picker>
      </view>
      <view class="i-carbon-chevron-down inline-block" />
      <!-- 班级 -->
      <view class="p-20rpx mr-30rpx inline-block b-1rpx b-white rounded-25rpx b-solid text-26rpx h-70rpx w-250rpx float-right" @change="bindClassChange">
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
    <!-- 日期天数 -->
    <view class="flex items-start">
      <view v-for="(item, index) in dayList" :key="item.id" model="dayList" :values="dayList" class="ml-40rpx inline-block">
        <view class="mt-77rpx rounded-20rpx flex-center h-66rpx w-66rpx" :style="[curDay === index ? 'backgroundColor:#00A76E;' : '']" @tap="curDay = index" @click="clickTab(index)">
          <text class="mt-21rpx text-36rpx">
            {{ item.day }}
          </text>
        </view>
        <view v-if="item.type === 0" class="mt-15rpx text-22rpx">
          三份作业
        </view>
      </view>
    </view>

    <!-- 作业功能 -->
    <view class="mt-38rpx text-center grid grid-cols-4">
      <view class="inline-block text-22rpx">
        <image src="../../static/images/10(6).png" class="h-100rpx w-120rpx" />
        <view class="mb-38rpx mt-20rpx text-center">
          发布作业
        </view>
      </view>
      <view class="inline-block text-22rpx">
        <image src="../../static/images/10(7).png" class="h-100rpx w-120rpx" />
        <view class="mb-38rpx mt-20rpx text-center">
          批改作业
        </view>
      </view>
      <view class="inline-block text-22rpx">
        <image src="../../static/images/10.png" class="h-100rpx w-120rpx" />
        <view class="mb-38rpx mt-20rpx text-center">
          发布学习计划
        </view>
      </view>
      <view class="inline-block text-22rpx">
        <image src="../../static/images/10(1).png" class="h-100rpx w-120rpx" />
        <view class="mb-38rpx mt-20rpx text-center">
          共性错题分析
        </view>
      </view>
      <view class="inline-block text-22rpx">
        <image src="../../static/images/10(5).png" class="h-100rpx w-120rpx" />
        <view class="mb-38rpx mt-20rpx text-center">
          离线批改
        </view>
      </view>
      <view class="inline-block text-22rpx">
        <image src="../../static/images/10(4).png" class="h-100rpx w-120rpx" />
        <view class="mb-38rpx mt-20rpx text-center">
          学情分析
        </view>
      </view>
      <view class="inline-block text-22rpx">
        <image src="../../static/images/10(2).png" class="h-100rpx w-120rpx" />
        <view class="mb-38rpx mt-20rpx text-center">
          挑题组卷
        </view>
      </view>
      <view class="inline-block text-22rpx">
        <image src="../../static/images/10(3).png" class="h-100rpx w-120rpx" />
        <view class="mb-38rpx mt-20rpx text-center">
          我的积分
        </view>
      </view>
    </view>
    <!-- 作业组件 -->
    <view>
      <view v-for="item in homeWordList" :key="item.id" class="px-25rpx pt-30rpx mb-30rpx bg-[#FFFFFF] rounded-10rpx h-290rpx w-690rpx" model="homeWordList" :value="homeWordList">
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
              <text>/{{ item.noCorrect }}</text>
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
  </view>
</template>

<style lang="less" scoped>
</style>
