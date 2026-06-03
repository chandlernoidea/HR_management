<template>
  <div class="tag-container">
    <transition-group name="tag" tag="div" class="tag">
      <el-tag
        size="mini"
        v-for="(item, index) in tagList"
        :key="item.code"
        :closable="item.code !== 'home'"
        :effect="$route.name === item.code ? 'dark' : 'plain'"
        :class="{ 'tag-active': $route.name === item.code }"
        @click="clickTag(item)"
        @close="closeTag(item, index)"
      >{{ item.name }}
      </el-tag>
    </transition-group>
  </div>
</template>

<script>

import { mapGetters } from 'vuex'

export default {
  name: 'Tag',
  computed: {
    ...mapGetters(['tagList'])
  },
  methods: {
    clickTag (item) {
      this.$router.push({
        name: item.code
      })
    },
    closeTag (item, index) {
      // 获取列表的最大索引值
      const maxIndex = this.tagList.length - 1
      if (item.code === this.$route.name) { // 判断关闭的标签是不是当前页，如果不是当前页，就直接关闭
        if (index === maxIndex) { // 如果关闭的标签是最右边的标签，就将页面跳转到相邻右侧的标签所示的页面
          this.$router.push({
            name: this.tagList[index - 1].code
          })
        } else {
          this.$router.push({
            name: this.tagList[index + 1].code
          })
        }
      }
      this.$store.commit('tag/CLOSE_TAG', item) // 关闭标签
    }
  }

}
</script>

<style lang="less" scoped>
.tag-container {
  padding: 8px 16px;
  background: var(--header-bg, #fff);
  border-bottom: 1px solid var(--border-color, #ebeef5);
  margin: 0;
}

.tag {
  display: flex;
  flex-wrap: wrap;
  gap: 8px;

  .el-tag {
    cursor: pointer;
    border-radius: 16px !important;
    transition: all 0.25s cubic-bezier(0.4, 0, 0.2, 1) !important;
    font-weight: 500;
    letter-spacing: 0.3px;
    border: 1px solid var(--border-color, #ebeef5) !important;
    background: #fff !important;

    &:hover {
      color: var(--color-primary, #409EFF) !important;
      border-color: var(--color-primary, #409EFF) !important;
      background: rgba(64, 158, 255, 0.06) !important;
      transform: translateY(-1px);
    }

    &.tag-active {
      background: var(--color-primary, #409EFF) !important;
      color: #fff !important;
      border-color: var(--color-primary, #409EFF) !important;
      box-shadow: 0 2px 8px rgba(64, 158, 255, 0.35);
    }
  }
}

// Tag transition animations
.tag-enter-active {
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}
.tag-leave-active {
  transition: all 0.2s cubic-bezier(0.4, 0, 0.2, 1);
}
.tag-enter {
  opacity: 0;
  transform: translateX(20px) scale(0.8);
}
.tag-leave-to {
  opacity: 0;
  transform: translateX(-10px) scale(0.8);
}
.tag-move {
  transition: transform 0.3s ease;
}
</style>
