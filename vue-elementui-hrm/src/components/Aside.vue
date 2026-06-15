<template>
  <el-menu
    default-active="2"
    class="el-menu-vertical-demo aside-menu"
    :collapse="isCollapsed"
    background-color="transparent"
    text-color="var(--sidebar-text, #bfcbd9)"
    active-text-color="var(--sidebar-active-text, #409EFF)"
  >
    <div class="aside-logo">
      <img
        src="../assets/logo.png"
        alt=""
        class="aside-logo-img"
      />
      <transition name="fade">
        <span v-if="!isCollapsed" class="aside-logo-text">
          人力资源管理系统
        </span>
      </transition>
    </div>
    <el-menu-item
      v-for="item in noChildren"
      :key="item.id"
      :index="item.name"
      @click="clickMenu(item,'/' + item.code)"
      class="aside-menu-item"
    >
      <i :class="'el-icon-' + item.icon"></i>
      <span slot="title"> {{ item.name }}</span>
    </el-menu-item>
    <el-submenu v-for="item in hasChildren" :key="item.id" :index="item.name" class="aside-submenu">
      <template slot="title">
        <i :class="'el-icon-' + item.icon"></i>
        <span>{{ item.name }}</span>
      </template>
      <el-menu-item
        v-for="subItem in item.children"
        @click="clickMenu(subItem,'/'+item.code + '/' + subItem.code)"
        :key="subItem.id"
        :index="subItem.name"
        class="aside-submenu-item"
      >
        <i :class="'el-icon-' + subItem.icon"></i>
        <span>{{ subItem.name }}</span>
      </el-menu-item>
    </el-submenu>
  </el-menu>
</template>

<style lang="less" scoped>
.aside-menu {
  height: 100%;
  border: none;
  background: linear-gradient(180deg, var(--sidebar-bg-start) 0%, var(--sidebar-bg-end) 100%) !important;
  transition: width 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  backdrop-filter: blur(10px);
  -webkit-backdrop-filter: blur(10px);

  &:not(.el-menu--collapse) {
    width: var(--sidebar-width);
    min-height: 400px;
  }
}

.aside-logo {
  height: var(--header-height);
  line-height: var(--header-height);
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 var(--spacing-lg);
  border-bottom: 1px solid rgba(255, 255, 255, 0.08);
  margin-bottom: var(--spacing-md);
  overflow: hidden;
  white-space: nowrap;
}

.aside-logo-img {
  width: 32px;
  height: 32px;
  flex-shrink: 0;
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.4));
  transition: transform var(--transition-fast);

  &:hover {
    transform: scale(1.05);
  }
}

.aside-logo-text {
  color: #FFFFFF;
  font-weight: 600;
  font-size: 13px;
  margin-left: var(--spacing-md);
  letter-spacing: 0.5px;
  overflow: hidden;
  text-overflow: ellipsis;
  opacity: 0.95;
}

// Menu items
.aside-menu-item,
/deep/ .el-submenu__title {
  transition: all var(--transition-fast) !important;
  position: relative;
  margin: 4px 8px;
  border-radius: 8px !important;
  font-size: 13px;

  &:hover {
    background-color: rgba(255, 255, 255, 0.1) !important;
  }

  &::before {
    content: '';
    position: absolute;
    left: 0;
    top: 50%;
    transform: translateY(-50%) scaleY(0);
    width: 3px;
    height: 50%;
    background: linear-gradient(180deg, var(--color-primary), var(--color-primary-light));
    border-radius: 0 3px 3px 0;
    transition: transform var(--transition-fast);
  }
}

// Active item with enhanced highlight
.aside-menu-item.is-active,
/deep/ .el-submenu .el-menu-item.is-active {
  background-color: rgba(0, 122, 255, 0.2) !important;
  color: #00D4FF !important;

  &::before {
    transform: translateY(-50%) scaleY(1);
  }
}

// Submenu items
.aside-submenu-item {
  margin: 3px 8px;
  border-radius: 6px;
  min-width: 0;
  font-size: 12px;

  &:hover {
    background-color: rgba(255, 255, 255, 0.08) !important;
  }
}

// Collapse transition
/deep/ .el-menu--collapse {
  .aside-logo {
    padding: 0;
  }

  .el-submenu__title,
  .el-menu-item {
    margin: 4px 4px;
  }
}

// Fade transition for logo text
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.3s ease;
}
.fade-enter,
.fade-leave-to {
  opacity: 0;
}
</style>

<script>
import { mapGetters } from 'vuex'

export default {
  name: 'Aside',
  methods: {
    clickMenu (menu, path) {
      this.$router.push({
        path: path
      })
      this.$store.commit('tag/ADD_TAG', menu)
    }
  },
  computed: {
    ...mapGetters(['menuList', 'isCollapsed']),
    noChildren () {
      return this.menuList.filter(item => item.children.length === 0)
    },
    hasChildren () {
      return this.menuList.filter(item => item.children.length > 0)
    }
  }
}
</script>
