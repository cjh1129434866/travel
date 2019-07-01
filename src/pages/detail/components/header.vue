<template>
   <div>
     <router-link tag="div" to="/" class="header-abc" v-show="showAbs">
       <div class="header-back-icon iconfont">
         &#xe629;
       </div>
     </router-link>
     <div class="header-fixed" v-show="!showAbs" :style="opacityStyle">
       景点详情
       <router-link to="/">
         <div class="header-back-fixed-icon iconfont">
           &#xe629;
         </div>
       </router-link>
     </div>
   </div>
</template>

<script>
export default {
  name: 'DetailHeader',
  data () {
    return {
      showAbs: true,
      opacityStyle: {
        opacity: 0
      }
    }
  },
  methods: {
    handleScroll () {
      const top = document.documentElement.scrollTop
      if (top > 60) {
        let opacity = top / 140
        opacity = opacity > 1 ? 1 : opacity
        this.opacityStyle = { opacity }
        this.showAbs = false
      } else {
        this.showAbs = true
      }
    }
  },
  activated () {
    window.addEventListener('scroll', this.handleScroll)
  },
  deactivated () {
    window.removeEventListener('scroll', this.handleScroll)
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
.header-abc
  position: absolute
  left: .2rem
  top: .2rem
  width: .8rem
  height: .8rem
  border-radius: 50%
  background: rgba(0, 0, 0, .8)
  color: #fff
  line-height: .8rem
  text-align: center
  .header-back-icon
    font-size: .4rem
.header-fixed
  z-index: 2
  position: fixed
  left: 0
  top: 0
  right: 0
  height: $headerHeight
  line-height: $headerHeight
  text-align: center
  color: #fff
  font-size: .32rem
  background: $bgColor
  .header-back-fixed-icon
    position: absolute
    top: 0
    width: .64rem
    font-size: .4rem
    color: #fff
    text-align: center
</style>
