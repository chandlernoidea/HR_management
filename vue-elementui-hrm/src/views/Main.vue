<template>
  <el-container style="height: 100%">
    <el-aside width="auto" class="layout-aside">
      <Aside/>
    </el-aside>
    <el-container class="layout-main-container">
      <el-header class="layout-header" height="60px">
        <Header/>
      </el-header>
      <Tag/>
      <el-main class="layout-main">
        <transition name="slide-up" mode="out-in">
          <router-view/>
        </transition>
      </el-main>
    </el-container>
  </el-container>
</template>

<script>

import Aside from '../components/Aside.vue'
import Header from '../components/Header.vue'
import Tag from '../components/Tag.vue'

export default {
  name: 'Main',
  components: {
    Aside,
    Header,
    Tag
  }
}
</script>

<style lang="less">
.layout-aside {
  box-shadow: 2px 0 12px rgba(0, 21, 41, 0.12);
  z-index: 10;
  overflow: hidden;
}

.layout-main-container {
  background-color: var(--content-bg, #f0f2f5);
}

.layout-header {
  background-color: var(--header-bg, #ffffff);
  box-shadow: var(--header-shadow, 0 1px 4px rgba(0, 21, 41, 0.08));
  z-index: 5;
  padding: 0 20px;
}

.layout-main {
  padding: 16px 20px;
  background-color: var(--content-bg, #f0f2f5);
  min-height: 0;
}

// Slide-up transition for page content
.slide-up-enter-active {
  transition: all 0.35s cubic-bezier(0.4, 0, 0.2, 1);
}
.slide-up-leave-active {
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
}
.slide-up-enter {
  transform: translateY(20px);
  opacity: 0;
}
.slide-up-leave-to {
  transform: translateY(-10px);
  opacity: 0;
}
</style>
