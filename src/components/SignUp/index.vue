<template>
  <div class="m-flexbox">
    <div class="m-flexitem">
      <el-col :span="24">
        <router-link to="/"><i class="el-icon-arrow-left m-btn-back"></i></router-link>
        <div class="m-form-wrapper">
          <el-form :model="ruleForm" :rules="rules" ref="ruleForm">
            <el-form-item prop="userName">
              <label for="userName">新用户账号</label>
              <el-input class="m-input-full-width m-input" v-model="ruleForm.userName"></el-input>
            </el-form-item>
            <el-form-item prop="password">
              <label for="password">密码</label>
              <el-input class="m-input-full-width m-input" type="password" v-model="ruleForm.password"></el-input>
            </el-form-item>
            <el-form-item prop="password2">
              <label for="password2">确认密码</label>
              <el-input class="m-input-full-width m-input" type="password" v-model="ruleForm.password2"></el-input>
            </el-form-item>
            <el-form-item class="m-center m-btn-wrapper">
              <el-button class="m-btn" type="primary" @click="submitForm('ruleForm')">注册</el-button>
            </el-form-item>
          </el-form>
        </div>
      </el-col>
    </div>
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
        this.$refs['ruleForm'].validate((flag, obj) => {
          if (!flag) {
            return
          }
          api.login()
        })
      }
    }
  }
</script>

<style scoped>
.m-flexbox {
  display: flex; 
  align-items: center; 
  justify-content: center; 
  height: 100vh;
  background: #666 url('../../assets/bg.png') no-repeat fixed center;
}

.m-flexitem {
  max-width: 16rem; 
  width: 100%; 
  background-color: #fff;
  padding: 2rem 4rem 7rem 4rem;
}

.m-btn-back {
  font-size: 2rem;
  color: #666;
}

label {
  color: #999;
}

.m-form-wrapper {
  margin-top: 4rem;
}

.m-input-full-width {
  width: 100%;
}

.m-input {
  color: #d0d0d0;
}

.m-center {
  text-align: center;
}

.m-middle {
  vertical-align: middle;
}

.m-btn-wrapper {
  margin-top: 3rem;
}

.m-btn {
  background-color: #00acac;
  border-radius: 0.7rem;
  max-width: 6rem;
  width: 100%;
  padding: 0.5rem 0.8rem;
}
</style>