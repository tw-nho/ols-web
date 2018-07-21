<template>
  <div>
    <el-col :span="8">&nbsp;</el-col>
    <el-col :span="8">
      <el-form :model="ruleForm" :rules="rules" ref="ruleForm">
        <el-form-item prop="userName">
          <label for="userName">用户名</label>
          <el-input class="m-input-full-width" v-model="ruleForm.userName"></el-input>
        </el-form-item>
        <el-form-item prop="password">
          <label for="password">密码</label>
          <el-input class="m-input-full-width" type="password" v-model="ruleForm.password"></el-input>
        </el-form-item>
        <el-form-item prop="password2">
          <label for="password2">确认密码</label>
          <el-input class="m-input-full-width" type="password" v-model="ruleForm.password2"></el-input>
        </el-form-item>
        <el-form-item class="m-center">
          <el-button class="m-btn" type="primary" @click="submitForm('ruleForm')">注册</el-button>
        </el-form-item>
        <el-form-item>
          <el-col :span="1">
            <router-link to="/">返回</router-link>
          </el-col>
        </el-form-item>
      </el-form>
    </el-col>
    <el-col :span="8">&nbsp;</el-col>
  </div>
</template>

<script>
  import api from '@/api'

  export default {
    data() {
      const validateRetypePasswordSame = (rule, value, callback) => {
        if (value !== this.ruleForm.password) {
          callback(new Error('Retyped password is different'))
        } else {
          callback()
        }
      }

      return {
        ruleForm: {
          userName: '',
          password: '',
          password2: '',
        },
        rules: {
          userName: [
            {required: true, message: '请输入用户名', trigger: 'blur'},
            {type: 'email', message: '请输入正确的邮箱地址', trigger: ['blur']},
          ],
          password: [
            {required: true, message: '请输入密码', trigger: 'blur'},
          ],
          password2: [
            {required: true, message: '请确认密码', trigger: 'blur'},
            {validator: validateRetypePasswordSame, message: '两次输入的密码不一致', trigger: ['blur']},
          ],
        }
      }
    },
    methods: {
      submitForm(formName) {
        api.login()
      }
    }
  }
</script>

<style>
.m-center {
  text-align: center;
}

.m-input-full-width {
  width: 100%;
}
</style>