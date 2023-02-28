<template>
  <view class="body_content">
    <view class="content">
      <view
        class="demo_item"
        v-for="item in list"
        @click="toListItem(item.path)"
      >
        <text class="title">{{ item.title }}</text>
        <text class="iconfont icon-youjiantou"></text>
      </view>
    </view>
  </view>
</template>

<script>
export default {
  data() {
    return {
      list: [
        {
          title: "引入ECharts",
          path: "/pages/echarts/echarts",
        },
        {
          title: "引入iconFont",
          path: "/pages/iconfont/iconfont",
        },
      ],
    };
  },
  onLoad() {},
  methods: {
    toListItem(url) {
      uni.navigateTo({
        url,
      });
    },
  },
};
</script>
<style>
page {
  background: #efe8e8b0;
}
</style>
<style lang="less" scoped>
view {
  box-sizing: border-box;
}
.body_content {
  padding: 32rpx;
}
.content {
  background: #fff;
}
.demo_item {
  padding: 15rpx 12rpx;
  border-bottom: solid 1rpx #ddd;
  display: flex;
  justify-content: space-between;
  align-items: center;
  .title {
    color: #000;
    font-size: 28rpx;
  }
}
</style>
