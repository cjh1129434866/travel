<template>
  <div class="icons">
    <swiper :options="swiperOption">
      <swiper-slide v-for="(item,index) in pages" :key="index">
        <div class="icon" v-for="iconItem in item" :key="iconItem.id">
          <div class="icon-img">
            <img class="icon-img-content" :src="iconItem.imgUrl" alt="">
          </div>
          <p class="img-des">{{iconItem.desc}}</p>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
export default {
  name: 'HomeIcons',
  props: {
    list: Array
  },
  data () {
    return {
      swiperOption: {
        autoplay: false
      }
    }
  },
  computed: {
    pages () {
      const pages = []
      this.list.forEach((item, index) => {
        const page = Math.floor(index / 8)
        if (!pages[page]) {
          pages[page] = []
        }
        pages[page].push(item)
      })
      return pages
    }
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
@import '~styles/mixins.styl'
.icons >>> .swiper-container
  padding-bottom: 50%
  width: 100%
  height: 0
  overflow: hidden
.icons
  marin-top: 0.1rem
  .icon
    position:relative
    float: left
    width: 25%
    height: 0
    overflow: hidden
    padding-bottom: 25%
    .icon-img
      position: absolute
      left: 0
      right: 0
      top: 0
      bottom: 0.44rem
      box-sizing: border-box
      padding: 0.1rem
      .icon-img-content
        display: block
        margin: 0 auto
        height: 100%
    .img-des
      position: absolute
      bottom: 0
      height: 0.44rem
      width: 100%
      line-height: 0.44rem
      text-align: center
      color : $darkTextColor
      overflow: hidden
      white-space : nowrap
      ellipsis()
</style>
