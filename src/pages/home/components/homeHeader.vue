<template>
  <div class="header">
    <div class="header-left">
      <div class="back-icon iconfont">
        &#xe629;
      </div>
    </div>
    <div class="header-input">
      <span class="iconfont">&#xe633;</span>
      输入城市景点/游玩
    </div>
    <router-link to="/city">
      <div class="header-right">
        {{this.city}}
        <span class="iconfont">&#xe600;</span>
      </div>
    </router-link>
  </div>
</template>

<script>
import { mapState } from 'vuex'
export default {
  name: 'HomeHeader',
  computed: {
    ...mapState(['city'])
  }
}
</script>

<!-- reset.css里面html的fontSize:50px = 1rem ;这里的设计图是苹果6的二倍图尺寸 -->
<!--

/*引入全局样式的方法*/
    /*方法一*/
   /*@import '../../../assets/styles/varibles.styl'*/
   /*方法二*/
     /*@import '~@/assets/styles/varibles.styl'*/
    /* 方法三就是再 webpack.base.conf 这个文件里面配置一个别名，就跟@的作用一样*/

 -->
<style lang="stylus" scoped>
  @import '~styles/varibles.styl'
  .header
    display: flex
    height: $headerHeight
    line-height: $headerHeight
    background: $bgColor
    color:#fff
    .header-left
      width: .64rem
      float:left
      text-align:center
      .back-icon
        font-size: .4rem
    .header-input
      flex: 1
      padding-left:0.2rem
      height: .64rem
      line-height: .64rem
      margin-top: .12rem
      margin-left: .2rem
      color: #ccc
      background: #fff
      border-radius: .1rem
    .header-right
      min-width: 1.04rem
      padding: 0 .1rem
      float: right
      text-align:center
      color: #fff
</style>
