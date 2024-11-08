<template>
  <RouterView></RouterView>
  <tab-bar v-if="!route.meta.hideTabBar"></tab-bar>
  <!-- <tab-bar></tab-bar> -->
</template>

<script setup>
import tabBar from './components/tab-bar/tab-bar.vue';
import {useRoute} from 'vue-router'

const route = useRoute()
</script>

<style scoped>

</style>
