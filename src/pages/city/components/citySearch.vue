<template>
  <div>
    <div class="search">
      <input v-model="inpVal" class="search-input" type="text" placeholder="输入城市名或拼音">
    </div>
    <div class="search-content" ref="search" v-show="inpVal">
      <ul>
        <li class="search-item border-bottom"
            v-for="item of list"
            :key="item.id"
            @click = 'handleCityClick(item.name)'
        >
          {{item.name}}
        </li>
        <li class="search-item border-bottom" v-show="hasNoData">没有任何匹配项</li>
      </ul>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'
import { mapMutations } from 'vuex'
export default {
  name: 'citySearch',
  props: {
    cities: Object
  },
  data () {
    return {
      list: [],
      timer: null,
      inpVal: ''
    }
  },
  mounted () {
    this.scroll = new BScroll(this.$refs.search)
  },
  computed: {
    hasNoData () {
      return !this.inpVal.length
    }
  },
  watch: {
    inpVal () {
      if (this.timer) {
        clearTimeout(this.timer)
      }
      if (!this.inpVal) {
        this.list = []
        return
      }
      this.timer = setTimeout(() => {
        const list = []
        for (let i in this.cities) {
          this.cities[i].forEach((item) => {
            if (item.spell.indexOf(this.inpVal) > -1 ||
              item.name.indexOf(this.inpVal) > -1
            ) {
              list.push(item)
            }
          })
        }
        this.list = list
      }, 100)
    }
  },
  methods: {
    handleCityClick (city) {
      this.changeCity(city)
      this.$router.push('/')
    },
    ...mapMutations(['changeCity'])
  }
}
</script>

<style lang="stylus" scoped>
@import '~styles/varibles.styl'
.search
  height: .72rem
  background: $bgColor
  padding: 0 .1rem
  .search-input
    box-sizing: border-box
    width: 100%
    height: .62rem
    line-height: .62rem
    padding: 0 .1rem
    border-radius: .1rem
    color: #666
    text-align: center
.search-content
  overflow: hidden
  position: absolute
  left: 0
  top: 1.58rem
  right: 0
  bottom: 0
  z-index: 1
  background: #eee
  .search-item
    line-height: .62rem
    padding-left: .2rem
    background: #fff
    color: #666
</style>
