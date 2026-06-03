<template>
  <div class="error-container">
    <div class="error-content">
      <div class="error-illustration">
        <img src="../../assets/images/404.png" alt="404" class="error-img"/>
      </div>
      <h2 class="error-title">页面未找到</h2>
      <p class="error-desc">抱歉，您访问的页面不存在或已被移除</p>
      <el-button type="primary" round class="error-btn" @click="goHome">
        <i class="el-icon-s-home"></i> 返回首页
      </el-button>
    </div>
  </div>
</template>
<script>
// 404页面
export default {
  name: 'Error',
  methods: {
    goHome () {
      this.$router.push('/home')
    }
  }
}
</script>
<style lang="less" scoped>
.error-container {
  display: flex;
  align-items: center;
  justify-content: center;
  min-height: calc(100vh - 200px);
  background: var(--content-bg, #f0f2f5);
}

.error-content {
  text-align: center;
  animation: bounce-in 0.8s cubic-bezier(0.4, 0, 0.2, 1) both;
}

.error-illustration {
  margin-bottom: 24px;
}

.error-img {
  width: 320px;
  height: auto;
  animation: float-gentle 4s ease-in-out infinite;
  filter: drop-shadow(0 8px 24px rgba(0, 0, 0, 0.1));
}

.error-title {
  font-size: 28px;
  font-weight: 700;
  color: var(--text-primary, #303133);
  margin: 0 0 12px;
  animation: stagger-in 0.5s ease both;
  animation-delay: 0.3s;
}

.error-desc {
  font-size: 15px;
  color: var(--text-secondary, #909399);
  margin: 0 0 32px;
  animation: stagger-in 0.5s ease both;
  animation-delay: 0.45s;
}

.error-btn {
  height: 44px;
  padding: 0 32px;
  font-size: 15px;
  font-weight: 600;
  animation: stagger-in 0.5s ease both;
  animation-delay: 0.6s;

  &:hover {
    transform: translateY(-2px);
    box-shadow: 0 6px 20px rgba(64, 158, 255, 0.35);
  }
}

@keyframes bounce-in {
  0% { transform: scale(0.3); opacity: 0; }
  50% { transform: scale(1.05); }
  70% { transform: scale(0.95); }
  100% { transform: scale(1); opacity: 1; }
}

@keyframes float-gentle {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-12px); }
}

@keyframes stagger-in {
  from { opacity: 0; transform: translateY(20px); }
  to { opacity: 1; transform: translateY(0); }
}
</style>
