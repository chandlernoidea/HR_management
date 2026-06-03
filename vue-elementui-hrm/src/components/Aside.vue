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
  background: linear-gradient(180deg, #1a1a2e 0%, #16213e 100%) !important;
  transition: width 0.3s cubic-bezier(0.4, 0, 0.2, 1);

  &:not(.el-menu--collapse) {
    width: 200px;
    min-height: 400px;
  }
}

.aside-logo {
  height: 60px;
  line-height: 60px;
  text-align: center;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 0 16px;
  border-bottom: 1px solid rgba(255, 255, 255, 0.06);
  margin-bottom: 8px;
  overflow: hidden;
  white-space: nowrap;
}

.aside-logo-img {
  width: 28px;
  height: 28px;
  flex-shrink: 0;
  filter: drop-shadow(0 2px 4px rgba(0, 0, 0, 0.3));
}

.aside-logo-text {
  color: #fff;
  font-weight: 700;
  font-size: 14px;
  margin-left: 8px;
  letter-spacing: 1px;
  overflow: hidden;
  text-overflow: ellipsis;
}

// Menu items
.aside-menu-item,
/deep/ .el-submenu__title {
  transition: all 0.25s ease !important;
  position: relative;
  margin: 2px 8px;
  border-radius: 6px;

  &:hover {
    background-color: rgba(255, 255, 255, 0.06) !important;
  }

  &::before {
    content: '';
    position: absolute;
    left: 0;
    top: 50%;
    transform: translateY(-50%) scaleY(0);
    width: 3px;
    height: 60%;
    background: linear-gradient(180deg, #409EFF, #66b1ff);
    border-radius: 0 3px 3px 0;
    transition: transform 0.25s ease;
  }
}

// Active item
.aside-menu-item.is-active,
/deep/ .el-submenu .el-menu-item.is-active {
  background-color: rgba(64, 158, 255, 0.15) !important;
  color: #409EFF !important;

  &::before {
    transform: translateY(-50%) scaleY(1);
  }
}

// Submenu items
.aside-submenu-item {
  margin: 2px 8px;
  border-radius: 6px;
  min-width: 0;

  &:hover {
    background-color: rgba(255, 255, 255, 0.06) !important;
  }
}

// Collapse transition
/deep/ .el-menu--collapse {
  .aside-logo {
    padding: 0;
  }

  .el-submenu__title,
  .el-menu-item {
    margin: 2px 4px;
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
