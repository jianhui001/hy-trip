<template>
  <div class="city">
    <div class="top">
      <van-search
        v-model="searchValue"
        shape="round"
        show-action
        placeholder="城市/区域/位置"
        @cancel="cancelClick"
      />
      <van-tabs v-model:active="tabActive" color="#ff9854">
        <template v-for="(value, key, index) in allCities">
          <van-tab :title="value.title" :name="key"></van-tab>
        </template>
      </van-tabs>
    </div>
    <div class="content">
      <!-- <cityGroup :groupData="currentGroup"></cityGroup> -->
      <template v-for="(value, key, index) in allCities">
        <cityGroup v-show="tabActive === key" :groupData="value"></cityGroup>
      </template>
    </div>
  </div>
</template>

<script setup>
import {ref, computed} from 'vue'
import {useRouter} from 'vue-router'
import { getCityAll } from '@/services';
import useCityStore from '@/stores/modules/city';
import { storeToRefs } from 'pinia';
import cityGroup from './cpns/city-group.vue';

const router = useRouter()

const searchValue = ref("")
const cancelClick = () => {
  router.back()
}

const tabActive = ref()

// const allCity = ref({})
// getCityAll().then(res => {
//   allCity.value = res.data
// })

const cityStore = useCityStore()
cityStore.fetchAllCitiesData()
const { allCities } = storeToRefs(cityStore)

// const currentGroup = computed(() => allCities.value[tabActive.value])

</script>

<style lang="less" scoped>
.city {
  // 顶部固定方案1
  // .top {
  //   position: fixed;
  //   top: 0;
  //   left: 0;
  //   right: 0;
  // }
  // .content {
  //   margin-top: 98px;
  // }
  // 顶部固定方案2
  .content {
    height: calc(100vh - 98px);
    overflow-y: auto;
  }
}
</style>