<template>
  <div class="search-box">
    <div class="location">
      <div class="city" @click="cityClick">{{ currentCity.cityName }}</div>
      <div class="position">
        <span class="text">我的位置</span>
        <img src="@/assets/img/home/icon_location.png" alt="" />
      </div>
    </div>
  </div>
</template>

<script setup>
import useCityStore from '@/stores/modules/city';
import { storeToRefs } from 'pinia';
import { useRouter } from 'vue-router';
const router = useRouter();

// 位置/城市
const cityClick = () => {
  router.push('/city');
};

const cityStore = useCityStore()
const {currentCity} = storeToRefs(cityStore)
</script>

<style lang="less" scoped>
.location {
  display: flex;
  align-items: center;
  padding: 0 20px;
  height: 44px;

  .city {
    flex: 1;
    color: #333;
    font-size: 15px;
  }

  .position {
    display: flex;
    align-items: center;
    width: 76px;

    .text {
      color: #666;
      font-size: 12px;
    }

    img {
      margin-left: 5px;
      width: 18px;
      height: 18px;
    }
  }
}
</style>
