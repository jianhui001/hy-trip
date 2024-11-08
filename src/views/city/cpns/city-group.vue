<template>
  <div class="city-group">
  <van-index-bar highlight-color="#ff9854" :index-list="indexList">
    <van-index-anchor index="热门" />
    <div class="list" >
      <template v-for="(item, index) in groupData.hotCities" :key="index">
        <div class="city" @click="cityClick(item)">{{ item.cityName }}</div>
      </template>
    </div>

    <template v-for="(item, index) in groupData.cities" :key="index">
      <van-index-anchor :index="item.group" />
      <template v-for="(city, num) in item.cities" :key="num">
        <van-cell :title="city.cityName" @click="cityClick(city)"/>
      </template>
     </template> 
    </van-index-bar>
  </div>
</template>

<script setup>
import useCityStore from '@/stores/modules/city';
import { computed } from 'vue';
import { useRouter } from 'vue-router';
const props = defineProps({
  groupData: {
    type: Object,
    default: () => ({}),
  },
});

const indexList = computed( () => {
  const list = props.groupData.cities.map( item => item.group)
  list.unshift("#")
  return list
})

const router = useRouter()
const cityStore = useCityStore()
const cityClick = (city) => {
  console.log("🚀 ~ cityClick ~ city:", city)
  cityStore.currentCity = city
  router.back()
}
</script>

<style lang="less" scoped>
.list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  padding: 10px;
  padding-right: 25px;
  .city {
    width: 70px;
    height: 28px;
    border-radius: 14px;
    font-size: 12px;
    color: #000;
    text-align: center;
    line-height: 28px;
    background-color: #fff4ec;
    margin: 6px 0;
  }
}
</style>
