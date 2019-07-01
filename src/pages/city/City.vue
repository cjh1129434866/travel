<template>
    <div>
      <CityHeader></CityHeader>
      <CitySearch :cities = 'cities'></CitySearch>
      <CityList
        :cities = 'cities'
        :hot="hotCities"
        :letter = 'letter'
      >
      </CityList>
      <CityAlphabet @change="handleLetter" :cities = 'cities'></CityAlphabet>
    </div>
</template>

<script>
import axios from 'axios'
import CityHeader from './components/cityHeader'
import CitySearch from './components/citySearch'
import CityList from './components/cityList'
import CityAlphabet from './components/Alphabet'

export default {
  name: 'City',
  data () {
    return {
      cities: {},
      hotCities: [],
      letter: ''
    }
  },
  components: {
    CityHeader,
    CitySearch,
    CityList,
    CityAlphabet
  },
  methods: {
    getCityInfo () {
      axios.get('/api/city.json')
        .then(this.handleGetCityInfoSucc)
    },
    handleGetCityInfoSucc (res) {
      res = res.data
      if (res.ret && res.data) {
        const data = res.data
        this.cities = data.cities
        this.hotCities = data.hotCities
      }
    },
    handleLetter (letter) { // 当前组件监听CityAlphabet组件触发的外部事件
      this.letter = letter
    }
  },
  mounted () {
    this.getCityInfo()
  }
}
</script>

<style scoped>

</style>
