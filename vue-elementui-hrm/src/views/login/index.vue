<template>
  <div class="login-wrapper">
    <!-- Animated Background -->
    <div class="login-bg">
      <div class="bg-shape shape-1"></div>
      <div class="bg-shape shape-2"></div>
      <div class="bg-shape shape-3"></div>
      <div class="bg-shape shape-4"></div>
      <div class="bg-shape shape-5"></div>
    </div>

    <!-- Login Card -->
    <div class="login-card">
      <div class="login-header">
        <img
          src="../../assets/logo.png"
          alt=""
          class="login-logo"
        />
        <h2 class="login-title">人力资源管理系统</h2>
        <p class="login-subtitle">Human Resource Management</p>
      </div>
      <el-form :rules="rules" :model="staff" ref="loginForm" class="login-form">
        <el-form-item prop="code">
          <el-input size="medium" placeholder="请输入账号" prefix-icon="el-icon-user"
                    v-model.trim="staff.code" class="login-input"></el-input>
        </el-form-item>
        <el-form-item prop="password" style="margin-top: 16px">
          <el-input size="medium" placeholder="请输入密码" prefix-icon="el-icon-lock" show-password
                    v-model.trim="staff.password" class="login-input"></el-input>
        </el-form-item>
        <el-form-item style="margin-top: 16px">
          <div class="captcha-row">
            <el-form-item prop="validateCode" style="flex: 1; margin-bottom: 0;">
              <el-input size="medium" placeholder="请输入验证码" prefix-icon="el-icon-key"
                        v-model.trim="staff.validateCode" class="login-input"></el-input>
            </el-form-item>
            <div class="login-code">
              <img ref="img" src="" @click="getCode" class="login-code-img" alt=""/>
            </div>
          </div>
        </el-form-item>
        <el-form-item style="margin-top: 24px">
          <el-button type="primary" size="medium" style="width:100%" @click="handleLogin" class="login-btn">
            登 录
          </el-button>
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>
<script>
import { login } from '@/api/login'
import { setValidateCode } from '@/utils/validateCode'

export default {
  name: 'Login',
  data () {
    return {
      staff: {},
      rules: {
        code: [
          { required: true, message: '请输入账号', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在3到10个字符', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' },
          { min: 3, max: 10, message: '长度在3到10个字符', trigger: 'blur' }
        ],
        validateCode: [
          { required: true, message: '请输入验证码', trigger: 'blur' }
        ]
      }
    }
  },
  mounted () {
    setValidateCode(this.$refs.img)
  },
  methods: {
    getCode () {
      setValidateCode(this.$refs.img)
    },
    handleLogin () {
      this.$refs.loginForm.validate(valid => {
        if (valid) {
          login(this.staff).then(
            response => {
              if (response.code === 200) {
                this.$store.commit('staff/SET_STAFF', response.data)
                this.$store.commit('token/SET_TOKEN', response.token)
                this.$message.success('登录成功！')
                this.$router.push({
                  path: '/home'
                })
              } else {
                this.$message.error(response.message)
              }
            }
          )
        } else {
          return false
        }
      })
    }
  }
}
</script>
<style lang="less" scoped>
.login-wrapper {
  height: 100vh;
  display: flex;
  align-items: center;
  justify-content: center;
  position: relative;
  overflow: hidden;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 25%, #f093fb 75%, #4facfe 100%);
  background-size: 400% 400%;
  animation: gradient-shift 15s ease infinite;
}

// Floating background shapes
.login-bg {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 0;
}

.bg-shape {
  position: absolute;
  border-radius: 50%;
  opacity: 0.08;
  background: #fff;

  &.shape-1 {
    width: 300px;
    height: 300px;
    top: -50px;
    left: -80px;
    animation: float-slow 20s ease-in-out infinite;
  }

  &.shape-2 {
    width: 200px;
    height: 200px;
    top: 50%;
    right: -60px;
    animation: float-medium 15s ease-in-out infinite;
    animation-delay: 2s;
  }

  &.shape-3 {
    width: 150px;
    height: 150px;
    bottom: -30px;
    left: 30%;
    animation: float-fast 12s ease-in-out infinite;
    animation-delay: 4s;
  }

  &.shape-4 {
    width: 100px;
    height: 100px;
    top: 20%;
    left: 15%;
    animation: float-medium 18s ease-in-out infinite;
    animation-delay: 1s;
  }

  &.shape-5 {
    width: 250px;
    height: 250px;
    bottom: 10%;
    right: 20%;
    animation: float-slow 22s ease-in-out infinite;
    animation-delay: 3s;
  }
}

// Glassmorphism card - macOS style
.login-card {
  position: relative;
  z-index: 1;
  width: 380px;
  padding: 40px;
  background: rgba(255, 255, 255, 0.18);
  backdrop-filter: blur(25px);
  -webkit-backdrop-filter: blur(25px);
  border-radius: 20px;
  border: 1px solid rgba(255, 255, 255, 0.25);
  box-shadow: 0 12px 40px rgba(0, 0, 0, 0.18);
  animation: card-slide-in 0.8s cubic-bezier(0.4, 0, 0.2, 1) both;
}

.login-header {
  text-align: center;
  margin-bottom: 32px;
}

.login-logo {
  width: 52px;
  height: 52px;
  margin-bottom: 16px;
  filter: drop-shadow(0 2px 8px rgba(0, 0, 0, 0.2));
  animation: pulse 3s ease-in-out infinite;
  transition: transform 0.3s ease;

  &:hover {
    transform: scale(1.05);
  }
}

.login-title {
  color: #fff;
  font-size: 24px;
  font-weight: 700;
  margin: 0 0 8px;
  text-shadow: 0 1px 2px rgba(0, 0, 0, 0.1);
  letter-spacing: 1px;
}

.login-subtitle {
  color: rgba(255, 255, 255, 0.8);
  font-size: 12px;
  margin: 0;
  letter-spacing: 0.5px;
  font-weight: 400;
}

.login-form {
  margin-top: 24px;
}

.login-input {
  /deep/ .el-input__inner {
    background: rgba(255, 255, 255, 0.2);
    border: 1px solid rgba(255, 255, 255, 0.3);
    color: #fff;
    border-radius: 12px;
    height: 44px;
    padding: 8px 12px;
    font-size: 13px;
    transition: all 0.3s ease;
    backdrop-filter: blur(10px);

    &::placeholder {
      color: rgba(255, 255, 255, 0.6);
    }

    &:focus {
      background: rgba(255, 255, 255, 0.3);
      border-color: rgba(255, 255, 255, 0.6);
      box-shadow: 0 0 0 2px rgba(255, 255, 255, 0.15);
    }

    &:hover {
      background: rgba(255, 255, 255, 0.25);
      border-color: rgba(255, 255, 255, 0.4);
    }
  }

  /deep/ .el-input__prefix {
    color: rgba(255, 255, 255, 0.7);
  }
}

.captcha-row {
  display: flex;
  align-items: flex-start;
  gap: 12px;
}

.login-code {
  flex-shrink: 0;
  width: 100px;
  height: 44px;
  border-radius: 12px;
  overflow: hidden;
  cursor: pointer;
  transition: all 0.2s ease;
  border: 1px solid rgba(255, 255, 255, 0.2);

  &:hover {
    transform: scale(1.02);
    border-color: rgba(255, 255, 255, 0.4);
  }

  img {
    width: 100%;
    height: 44px;
    border-radius: 12px;
    display: block;
    object-fit: cover;
  }
}

.login-btn {
  height: 44px !important;
  font-size: 15px !important;
  font-weight: 600 !important;
  letter-spacing: 2px;
  border-radius: 12px !important;
  background: linear-gradient(135deg, rgba(255, 255, 255, 0.3), rgba(255, 255, 255, 0.15)) !important;
  border: 1px solid rgba(255, 255, 255, 0.4) !important;
  color: #fff !important;
  backdrop-filter: blur(10px);
  transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1) !important;

  &:hover {
    background: linear-gradient(135deg, rgba(255, 255, 255, 0.4), rgba(255, 255, 255, 0.2)) !important;
    box-shadow: 0 8px 32px rgba(0, 0, 0, 0.2);
    transform: translateY(-2px);
  }

  &:active {
    transform: translateY(0) scale(0.98);
  }
}

@keyframes gradient-shift {
  0% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
  100% { background-position: 0% 50%; }
}

@keyframes float-slow {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  33% { transform: translateY(-20px) rotate(5deg); }
  66% { transform: translateY(10px) rotate(-3deg); }
}

@keyframes float-medium {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50% { transform: translateY(-30px) rotate(-8deg); }
}

@keyframes float-fast {
  0%, 100% { transform: translateY(0) translateX(0); }
  25% { transform: translateY(-15px) translateX(10px); }
  75% { transform: translateY(15px) translateX(-10px); }
}

@keyframes card-slide-in {
  from {
    opacity: 0;
    transform: translateY(40px) scale(0.95);
  }
  to {
    opacity: 1;
    transform: translateY(0) scale(1);
  }
}

@keyframes pulse {
  0%, 100% { transform: scale(1); }
  50% { transform: scale(1.08); }
}
</style>
