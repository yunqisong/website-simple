<script setup>
import CommonHeader from "./CommonHeader.vue";
import {ref} from 'vue'
</script>

<template>
  <router-view v-slot="{ Component }">
    <transition>
      <keep-alive>
        <component
          :is="Component"
          class="main-content"
          :key="$route.fullPath"
        />
      </keep-alive>
    </transition>
  </router-view>
  <!-- <div class="" style="height: 100vh;">
    <iframe
      v-resize="{ log: true }"
      width="100%"
      height="100%"
      :src="iframeUrl"
      frameborder="0"
    ></iframe>
  </div> -->
</template>

<style scoped>
a {
  color: #42b983;
}

.main-content {
  min-height: 500px;
}
</style>
