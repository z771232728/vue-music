<template>
  <!--小播放器圆心播放进度组件-->
  <div class="progress-circle">
    <svg :width="radius" :height="radius" viewBox="0 0 100 100" version="1.1" xmlns="http://www.w3.org/2000/svg">
      <circle class="progress-background" r="50" cx="50" cy="50" fill="transparent"></circle>

      <!--stroke-dasharray 描边距-->
      <!--stroke-dashoffset 描边偏移 （覆盖）0全覆盖 314==无覆盖 -->

      <circle class="progress-bar" r="50" cx="50" cy="50" fill="transparent"
      :stroke-dasharray="dashArray"
      :stroke-dashoffset="dashOffset"
      ></circle>
    </svg>
    <!--插槽-->
    <slot></slot>
  </div>
</template>

<script type="text/ecmascript-6">
  export default {
    props: {
      radius: {
        type: Number,
        default: 100
      },
      percent: {
        type: Number,
        default: 0
      }
    },
    data() {
      return {
        dashArray: Math.PI * 100 // 取周长
      }
    },
    computed: {
      dashOffset () {
//        播放比最大是1 减去总比 乘周长
        return (1 - this.percent) * this.dashArray // 取已经播放的进度 占周长的比例
      }
    }
  }
</script>

<style lang="stylus" rel="stylesheet/stylus">
  @import "~common/stylus/variable"

  .progress-circle
    position relative
    circle
      stroke-width: 8px
      transform-origin: center
      &.progress-background
        transform: scale(0.9)
        stroke: $color-theme-d
      &.progress-bar
        transform: scale(0.9) rotate(-90deg)
        stroke: $color-theme
</style>
