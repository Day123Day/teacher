<script setup lang="ts">
import { ref } from 'vue'
import { Fetch } from '~/utils/fetch'
import $bus from '~/pages/bus/bus'

const dayList: any = ref([])
const curDay = ref(0)

// tab切换
function clickTab(index: number) {
  // console.log(item.day)
  // Fetch('http://127.0.0.1:8081/api/day', { data: { day: day }, method: 'POST' })

  Fetch('http://127.0.0.1:8081/api/dayList', { method: 'GET' }).then((res) => {
    $bus.emit('getHomeWordList', res[index].homeWordList)
  })
}

Fetch('http://127.0.0.1:8081/api/dayList', { method: 'GET' }).then((res) => {
  dayList.value = res
  $bus.emit('getHomeWordList', res[0].homeWordList)
})
</script>

<template>
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
</template>

<style>

</style>
