<template>
  <div class="tab-bar">
    <van-tabbar v-model="currentIndex" active-color="#ff9854">
      <template v-for="(item, index) in tabbarData">
        <van-tabbar-item :to="item.path">
          <span>{{ item.text }}</span>
          <template #icon>
            <img v-if="currentIndex !== index" :src="getAssetURL(item.image)" />
            <img v-else :src="getAssetURL(item.imageActive)" />
          </template> 
        </van-tabbar-item>
      </template>
    </van-tabbar>

    <!-- <template v-for="(item, index) in tabbarData">
      <div 
        class="tab-bar-item"
        :class="currentIndex === index ? 'active' : ''"
        @click="itemClick(index, item)"
      >
        <img v-if="currentIndex !== index" :src="getAssetURL(item.image)" />
        <img v-else :src="getAssetURL(item.imageActive)" />
        <span class="text">{{ item.text }}</span>
      </div>
    </template> -->
  </div>
</template>

<script setup>
import tabbarData from '@/assets/data/tabbar';
import { getAssetURL } from '@/utils/load_assets';
import { ref } from 'vue';
import { useRouter } from 'vue-router';

const currentIndex = ref(0);
const router = useRouter();
const itemClick = (index, item) => {
  currentIndex.value = index;
  router.push(item.path);
};
</script>

<style lang="less" scoped>
// .tab-bar {
//   position: fixed;
//   left: 0;
//   right: 0;
//   bottom: 0;
//   height: 50px;
//   border-top: solid 1px #f3f3f3;

//   display: flex;
//   .tab-bar-item {
//     flex: 1;
//     display: flex;
//     flex-direction: column;
//     justify-content: center;
//     align-items: center;

//     &.active {
//       color: var(--primary-color);
//     }
//     img {
//       width: 26px;
//       padding-bottom: 2px;
//     }
//     text {
//       // font-size: ;
//     }
//   }
// }
.tab-bar {
  img {
    height: 26px;
  }
}
</style>
