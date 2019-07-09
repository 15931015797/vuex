<template>
<div class="login">
    <van-nav-bar title="登录"/>
    <!-- 表单 -->
    <form>
        <van-cell-group>
            <van-field
                v-model="user.mobile"
                required
                clearable
                label="手机号"
                placeholder="请输入手机号"
                :error-message="errors.mobile"
            />

            <van-field
                v-model="user.code"
                type="password"
                label="密码"
                placeholder="请输入密码"
                :error-message="errors.code"
                required
            />
        </van-cell-group>
        <div class="login-btn-box">
            <van-button
            class="login-btn"
            type="info"
            :loading="loginLoading"
            loading-text="登录中..."
            @click.prevent="handleLogin"
            >登录</van-button>
        </div>
    </form>
</div>
</template>

<script>
import { login } from '@/api/user'
export default {
  data () {
    return {
      user: {
        mobile: '15931015797',
        code: '123456'
      },
      loginLoading: false,
      errors: {
        mobile: '',
        code: ''
      }
    }
  },
  methods: {
    async handleLogin () {
      try {
        const { mobile, code } = this.user
        const errors = this.errors
        if (mobile.length) {
          errors.mobile = ''
        } else {
          errors.mobile = '手机号不能为空'
          return
        }
        if (code.length) {
          errors.code = ''
        } else {
          errors.code = '验证码不能为空'
          return
        }
        this.loginLoading = true
        const data = await login(this.user)
        this.$store.commit('setUser', data)
        this.$router.push({
          name: 'home'
        })
      } catch (err) {
        console.log(err)
        console.log('登录失败')
      }
      this.loginLoading = false
    }
  }
}
</script>

<style lang="less" scoped>
.login-btn-box{
    padding: 20px;
    .login-btn{
        width: 100%;
    }
}
</style>
