<template>
  <view>
    <view>微信小程序使用iconfont图标 </view>
    <view class="iconfont icon-wodedingdan"></view>
    <view class="iconfont icon-wode"></view>
  </view>
</template>

<script>
export default {
  name: "name",
  components: {},
  props: {
    list: {
      type: Array,
      default: () => [],
    },
  },
  data() {
    return {};
  },
  computed: {},
  watch: {},
  methods: {},
};
</script>
<style lang='scss' scoped>
.iconfont {
  font-size: 60rpx;
}
</style>