<template>
  <div class="header">
    城市选择
    <router-link to="/">
      <div class="back-icon iconfont">
        &#xe629;
      </div>
    </router-link>
  </div>
</template>

<script>
export default {
  name: 'cityHeader'
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
.header
  position: relative
  overflow: hidden
  height: $headerHeight
  line-height: $headerHeight
  text-align: center
  color: #fff
  font-size: .32rem
  background: $bgColor
  .back-icon
    position: absolute
    top: 0
    width: .64rem
    font-size: .4rem
    color: #fff
    text-align: center
</style>
