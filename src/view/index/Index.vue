<script setup>
import AdSideC from '@/components/AdSideC.vue'
import SiteListO from '@/components/SiteListO.vue'
import TodayHotNews from '@/components/TodayHotNews.vue'
import SiteRtypesQlist from '@/components/SiteRtypesQlist.vue'
import SiteTypesListN from '@/components/SiteTypesListN.vue'
import RecomNews from '@/components/RecomNews.vue'
import RecomSoft from '@/components/RecomSoft.vue'
import CommonHeader from '@/components/CommonHeader.vue'
import AdRow from "@/components/AdRow.vue";
import AdFoot from "@/components/AdFoot.vue";
import CommonFooter from "@/components/CommonFooter.vue";
import {ref, computed} from 'vue'

const first = ref(null);
const pro1 = axios.get("/api/base/first").then((res) => {
  first.value = res.data.data;
  return res
});

const second = ref(null);
const pro2 = axios.get("/api/base/second").then((res) => {
  second.value = res.data.data;
  return res
});

const third = ref(null);
const pro3 = axios.get("/api/base/third").then((res) => {
  third.value = res.data.data;
  return res
});

const fourth = ref(null);
const pro4 = axios.get("/api/base/fourth").then((res) => {
  fourth.value = res.data.data;
  return res
});

const loadStatus = ref(false)
const pros = () => {
  Promise.all([pro1, pro2, pro3, pro4]).then(ress => {
    console.log(ress, '请求完毕')
    loadStatus.value = true
    showScreenAdFn();
  })
}

const showScreenAdStatus = ref(false)
const showScreenAdFn = () => {
  setTimeout(() => {
    showScreenAdStatus.value = true
  }, 3000)
}

pros();
</script>

<template>
  <div
    class="index-frame"
    v-if="!loadStatus"
    v-loading="!loadStatus"
    style="height: 100vh"
  ></div>
  <div v-else>
    <AdRow :data="first.a"/>

    <div style="position: relative;">
      <CommonHeader :data="second"/>
      <div class="ad-d">
        <AdRow :data="first.d"/>
      </div>
    </div>

    <div class="main">
      <div class="sidebar">
        <AdSideC :data="first.c"/>

        <SiteTypesListN :data="third.n"/>

        <div class="m-bt-15">
          <RecomNews/>
        </div>

        <div class="m-bt-15">
          <RecomSoft :data="third.p"/>
        </div>
      </div>

      <div class="container">
        <SiteListO :data="third.o"/>

        <!-- 今日热点 -->
        <div class="m-bt-15">
          <TodayHotNews/>
        </div>

        <!-- 网站分类 -->
        <div class="m-bt-15">
          <SiteRtypesQlist :dataR="third.r" :dataQ="third.q"/>
        </div>
      </div>
    </div>

    <!-- 版权信息 -->
    <div class="m-t-15">
      <CommonFooter :data="fourth"/>
    </div>
    
    <!-- 底部广告 -->
    <div class="showCopyRight" style="z-index: 15;">
      <AdRow :data="first.e"/>
    </div>

    <!-- 两边的广告 -->
    <div class="ad-b ad-b--l">
      <AdRow :data="first.b[0]"/>
    </div>
    <div class="ad-b ad-b--r">
      <AdRow :data="first.b[1]"/>
    </div>

    <!-- 开屏广告 -->
    <div v-if="showScreenAdStatus">
      <AdFoot :data="first.f"/>
    </div>
  </div>
  
</template>

<style lang="less" scoped>
.main {
  width: 1180px;
  margin: auto;
  display: flex;
  justify-content: space-between;
  .sidebar {
    flex-basis: 282px;
    flex-shrink: 0;
    overflow: hidden;
  }
  .container {
    flex-basis: 887px;
    flex-shrink: 0;
    flex-grow: 0;
    margin: 0;
  }
}
.ad-d {
  position: absolute;
  top: 0;
  right: 0;
  width: 112px;
  height: 98px;
  object-fit: cover;
}

@media only screen
  and (min-width: 1500px) {
    .ad-b { 
      width: 330px !important;
      height: 330px !important;
    }
}

.ad-b {
  position: fixed;
  width: 100px;
  height: 100px;
  z-index: 999;
  &--l {
   top: 300px;
   left: 22px;
  }
  &--r {
    bottom: 200px;
    right: 22px;
  }
}

.showCopyRight {
  position: fixed;
  bottom: 0;
  left: 0;
  right: 0;
  z-index: 12;
}
</style>
