<template>
  <!-- 背景图 -->
  <div class="picture">
    <!-- 中间的白色卡片 -->
    <el-card class="login-card">
      <!-- 黑马头条logo -->
      <div class="title">
        <img src="../../assets/img/logo_index.png" alt />
      </div>
      <el-form :model="formData" :rules="rules" ref="loginForm">
        <el-form-item prop="mobile">
          <el-input placeholder="请输入手机号" v-model="formData.mobile"></el-input>
        </el-form-item>
        <el-form-item prop="code">
          <el-input placeholder="请输入验证码" class="yz" v-model="formData.code"></el-input>
          <el-button style="float:right">发送验证码</el-button>
        </el-form-item>
        <el-form-item>
          <el-checkbox v-model="formData.check">我已阅读并同意用户协议和隐私条款</el-checkbox>
        </el-form-item>
        <el-form-item>
          <el-button @click="login" type="primary" style="width:100%">登录</el-button>
        </el-form-item>
      </el-form>
    </el-card>
  </div>
</template>

<script>
export default {
  data () {
    var func = function (rule, value, callback) {
      if (value) {
        callback()
      } else {
        callback(new Error('您必须无条件同意被坑'))
      }
    }
    return {
      formData: {
        mobile: '',
        code: '',
        check: false
      },
      rules: {
        mobile: [
          {
            required: true,
            message: '登录手机号不能为空',
            tigger: 'blur'
          },
          { pattern: /^1[3456789]\d{9}$/, message: '手机号格式错误' }
        ],
        code: [
          {
            required: true,
            message: '验证码不能为空',
            trigger: 'blur'
          },
          { parttern: /^\d{6}$/, message: '验证码必须为6位数字' }
        ],
        check: [
          {
            validator: func
          }
        ]
      }
    }
  }
}
</script>

<style lang ='less' scoped>
.picture {
  width: 100%;
  height: 100vh;
  background: url("../../assets/img/login_bg.jpg");
  background-size: cover;
  display: flex;
  justify-content: center;
  align-items: center;
  .login-card {
    width: 440px;
    height: 360px;
    .title {
      text-align: center;
      margin-bottom: 30px;
      img {
        width: 200px;
        height: 45px;
      }
    }
    .yz {
      width: 65%;
    }
  }
}
</style>
