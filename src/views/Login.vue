<template>
  <div class="login_container">
    <div class="login_box">
      <div class="login_title">
        <span class="title">数据管理平台</span>
        <el-form ref="loginFormRef" :model="loginForm" :rules="loginFormRules" label-width="0px">
          <!-- 用户名 -->
          <el-form-item prop="username">
            <el-input
              prefix-icon="fa fa-user-circle"
              placeholder="请输入账号"
              v-model="loginForm.username"
            ></el-input>
          </el-form-item>
          <!-- 密码 -->
          <el-form-item prop="password">
            <el-input
              prefix-icon="fa fa-lock"
              type="password"
              placeholder="请输入密码"
              v-model="loginForm.password"
            ></el-input>
          </el-form-item>
          <!-- 按钮区域 -->
          <el-form-item class="btns">
            <el-button type="primary" @click="login">登录</el-button>
          </el-form-item>
        </el-form>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data: function () {
    return {
      loginForm: {
        username: '',
        password: ''
      },
      loginFormRules: {
        username: [
          { required: true, message: '请输入用户名', trigger: 'blur' },
          { min: 3, max: 10, message: '长度为3到10位', trigger: 'blur' }
        ],
        password: [
          { required: true, message: '请输入密码', trigger: 'blur' }
        ]
      }
    }
  },
  methods: {
    login () {
      // 表单验证
      this.$refs.loginFormRef.validate(async valid => {
        if (!valid) return
        const { data: res } = this.$http.post('login', this.loginForm)
        if (res.meta.status !== 200) return this.$message.error('登录失败')
        this.$message.success('登录成功')
        // window.sessionStorage.setItem('token', res.data.token)
        this.$router.push('/home')
      })
    }
  }
}
</script>

<style lang="less" scoped>
.login_container {
  height: 100%;
  background-image: url("../assets/images/login.png");
  background-size: 100%;
}
.login_box {
  width: 1103px;
  height: 613px;
  background-image: url("../assets/images/login-background.png");
  background-size: 100%;
  // border-radius: 3px;
  position: absolute;
  left: 50%;
  top: 50%;
  // background-color: #fff;
  transform: translate(-50%, -50%);
}
.login_title {
  text-align: center;
  width: 325px;
  height: 300px;
  position: relative;
  left: 665px;
  top: 116px;
}
.title {
  font-size: 25px;
  font-weight: 1000;
  color: #006cde;
  letter-spacing: 8px;
  margin-bottom: 20px;
}

.el-button {
  width: 100%;
}

.el-form {
  margin-top: 20px;
}
</style>
