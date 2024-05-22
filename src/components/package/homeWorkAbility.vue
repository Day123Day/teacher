<script setup lang="ts">
const imgURL = '../../static/images/'
const proxyList = [
  {
    name: '发布作业',
    img: `${imgURL}10(6).png`,
  },
  {
    name: '批改作业',
    img: `${imgURL}10(7).png`,
  },
  {
    name: '发布学习计划',
    img: `${imgURL}10.png`,
  },
  {
    name: '共性错题分析',
    img: `${imgURL}10(1).png`,
  },
  {
    name: '离线批改',
    img: `${imgURL}10(5).png`,
  },
  {
    name: '学情分析',
    img: `${imgURL}10(4).png`,
  },
  {
    name: '挑题组卷',
    img: `${imgURL}10(2).png`,
  },
  {
    name: '我的积分',
    img: `${imgURL}10(3).png`,
  },
]
</script>

<template>
  <view class="mt-38rpx text-center grid grid-cols-4">
    <view v-for="(item, index) in proxyList" :key="index" class="inline-block text-22rpx">
      <image :src="item.img" class="h-100rpx w-120rpx" />
      <view class="mb-38rpx mt-20rpx text-center">
        {{ item.name }}
      </view>
    </view>
  </view>
</template>

<style>

</style>
