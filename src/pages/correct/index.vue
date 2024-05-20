<script setup lang="ts">
import type { ECOption } from '~/widgets/guodu-echarts/echarts'

const chartData1 = ref<ECOption>({
  tooltip: {
    trigger: 'axis',
    axisPointer: {
      // 坐标轴指示器，坐标轴触发有效
      type: 'shadow', // 默认为直线，可选为：'line' | 'shadow'
    },
    confine: true,
  },
  legend: {
    data: [
      {
        name: '正确人数',
        itemStyle: {
          borderWidth: 2,
          borderColor: '#00A76E',
        },
      },
      {
        name: '错误人数',
        itemStyle: {
          borderWidth: 2,
          borderColor: '#FF485E',
        },
      },
    ],
    icon: 'circle',
    itemStyle: {
      color: '#FFFFFF',
    },
    bottom: '5%',
  },
  grid: {
    left: 5,
    right: 20,
    bottom: 55,
    top: 40,
    containLabel: true,
  },
  title: {
    text: '数据统计',
  },
  xAxis: {
    type: 'category',
    data: ['第1题', '第2题', '第3题', '第4题', '第5题', '第6题', '第7题'],
  },
  yAxis: {
    type: 'value',
  },
  // 数据
  series: [
    {
      name: '正确人数',
      data: [20, 30, 40, 50, 60, 55, 40],
      type: 'bar',
      color: '#00A76E',
      itemStyle: {
        borderRadius: [10, 10, 0, 0], // 设置圆角半径
      },
      showBackground: true,
    },
    {
      name: '错误人数',
      data: [30, 40, 50, 60, 70, 10, 20],
      type: 'bar',
      color: '#FF485E',
      itemStyle: {
        borderRadius: [10, 10, 0, 0], // 设置圆角半径
      },
      showBackground: true,
    },
  ],
})
const chartData2 = ref<ECOption>({
  series: [
    {

      itemStyle: {
        color: 'white',
      },
      // 缩放
      radius: '100%',
      type: 'gauge',
      axisLine: {
        lineStyle: {
          width: 5,
          color: [
            [1, '#1D8C66'],
          ],
        },
      },
      pointer: {
        show: false,
      },
      // 覆盖的颜色的显示和跨度
      progress: {
        show: true,
        width: 5,
      },
      // 控制内圈短线
      axisTick: {
        splitNumber: 0,
        lineStyle: {
          width: 0,
        },
      },
      // 内圈长线
      splitLine: {
        length: 0,
      },
      // 内圈数字
      axisLabel: {
        fontSize: 0,
      },
      // 控制字体颜色位置
      detail: {
        offsetCenter: [0, '0%'],
        fontSize: 15,
        formatter: '{value}%',
        color: 'white',
      },
      data: [
        {
          value: 85,
        },
      ],
    },
  ],
})
</script>

<template>
  <view class="bg-[#F5F5F9]">
    <!-- 上 -->
    <view class="px-30rpx pt-110rpx bg-[#00A76E] h-540rpx w-750rpx">
      <!-- 第一 -->
      <view class="w-750rpx">
        <view class="i-carbon-chevron-left mr-249rpx inline-block text-color h-30rpx w-34rpx" />
        <text class="text-32rpx text-center text-color">
          批改详情
        </text>
      </view>
      <!-- 第二 -->
      <view class="mt-60rpx flex h-44rpx items-center">
        <text class="text-32rpx text-color">
          10/07·初中数学
        </text>
        <view class="ml-30rpx inline-block b-2rpx b-[#FFFFFF] rounded-22rpx b-solid flex flex-center h-44rpx w-120rpx">
          <text class="text-20rpx text-center text-color">
            基础作业
          </text>
        </view>
      </view>
      <!-- 第三 -->
      <view class="w-690rpx">
        <view class="inline-block text-color">
          <view class="mt-57rpx text-24rpx">
            班级：五年级一班 数学
          </view>
          <view class="mt-37rpx text-24rpx">
            辅码：一人一码
          </view>
          <view class="mt-37rpx text-24rpx">
            时间：10/10 12:00 — 10/20 12:00
          </view>
        </view>
        <!-- 上图表 -->
        <view class="ml-120rpx inline-block text-center h-125rpx w-156rpx">
          <GuoduEcharts
            :options="chartData2" canvas-id="chartData2"
          />
          <text class="text-22rpx text-color">
            平均得分率
          </text>
        </view>
      </view>
    </view>
    <!-- 中间图表 -->
    <view class="pb-35rpx pl-30rpx pt-50rpx mt-[-30rpx] bgcolor border-rounded text-20rpx h-560rpx w-750rpx">
      <GuoduEcharts
        :options="chartData1" canvas-id="chartData1"
      />
    </view>
    <!-- 卡片区域 -->
    <view class="px-30rpx pt-40rpx mt-25rpx bgcolor border-rounded h-250rpx w-750rpx">
      <view>
        <text class="text-30rpx font-600">
          最高得分率
        </text>
        <text class="text-38rpx font-600 c-[#00A76E] float-right">
          75%
        </text>
      </view>
      <view class="grid grid-cols-3">
        <view class="mt-40rpx">
          <view class="i-carbon-user-filled mr-18rpx inline-block c-[#A9BCD3]" />
          <text class="text-28rpx c-[#465A7B]">
            陈小胖
          </text>
        </view>
        <view class="mt-40rpx">
          <view class="i-carbon-user-filled mr-18rpx inline-block c-[#A9BCD3]" />
          <text class="text-28rpx c-[#465A7B]">
            陈小胖
          </text>
        </view>
        <view class="mt-40rpx">
          <view class="i-carbon-user-filled mr-18rpx inline-block c-[#A9BCD3]" />
          <text class="text-28rpx c-[#465A7B]">
            陈小胖
          </text>
        </view>
        <view class="mt-40rpx">
          <view class="i-carbon-user-filled mr-18rpx inline-block c-[#A9BCD3]" />
          <text class="text-28rpx c-[#465A7B]">
            陈小胖
          </text>
        </view>
        <view class="mt-40rpx">
          <view class="i-carbon-user-filled mr-18rpx inline-block c-[#A9BCD3]" />
          <text class="text-28rpx c-[#465A7B]">
            陈小胖
          </text>
        </view>
      </view>
    </view>
    <view class="px-30rpx pt-40rpx mt-25rpx bgcolor border-rounded h-180rpx w-750rpx">
      <view>
        <text class="text-30rpx font-600">
          最高得分率
        </text>
        <text class="text-38rpx font-600 c-[#FC5260] float-right">
          25%
        </text>
      </view>
      <view class="grid grid-cols-3">
        <view class="mt-40rpx">
          <view class="i-carbon-user-filled mr-18rpx inline-block c-[#A9BCD3]" />
          <text class="text-28rpx c-[#465A7B]">
            陈小胖
          </text>
        </view>
      </view>
    </view>
    <!-- end -->
    <view class="px-30rpx pt-40rpx mt-25rpx bgcolor border-rounded rounded-b-0rpx h-520rpx w-750rpx">
      <view class="mb-40rpx text-28rpx">
        <text class="mr-41rpx c-[#00A76E]">
          有错
        </text>
        <text class="mr-41rpx">
          全对
        </text>
        <text class="mr-41rpx">
          部分批改
        </text>
        <text class="mr-41rpx">
          未批改
        </text>
      </view>
      <view>
        <view class="py-22rpx b-b-1rpx b-b-[#E8EAF1] b-b-solid text-24rpx c-[#8F9AA8] grid grid-cols-3">
          <text>学生姓名</text>
          <text>批改状态</text>
          <text>正确率</text>
        </view>
        <view class="py-22rpx b-b-1rpx b-b-[#E8EAF1] b-b-solid text-24rpx grid grid-cols-3">
          <text>周小虎</text>
          <text>已批改</text>
          <text class="c-[#3FB385]">
            98%
          </text>
        </view>
        <view class="py-22rpx b-b-1rpx b-b-[#E8EAF1] b-b-solid text-24rpx grid grid-cols-3">
          <text>李冬冬</text>
          <text>已批改</text>
          <text class="c-[#3FB385]">
            98%
          </text>
        </view>
        <view class="py-22rpx b-b-1rpx b-b-[#E8EAF1] b-b-solid text-24rpx grid grid-cols-3">
          <text>韩菲菲</text>
          <text class="c-[#FF8400]">
            未批改
          </text>
          <text class="c-[#3FB385]">
            --
          </text>
        </view>
      </view>
    </view>
  </view>
</template>

<style>

</style>
