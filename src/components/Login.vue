<template>
  <div class="hello">
    <link rel="stylesheet" href="../css/common.css">
    <!-- <h1>{{ msg }}</h1> -->
    <!-- <h2>Essential Links</h2> -->
    <!-- <img class="bgImg" src="/static/images/500074312.jpg" alt=""> -->
    <div class="main">
      <img class="redius showImg" src="/static/images/photo0000-3530.jpg" alt="">
      <el-form :model="loginForm" :rules="rules1" ref="loginForm" label-width="100px" id="loginForm">
        <el-form-item label="账号">
          <el-input v-model="loginForm.ID" placeholder="11位手机号 或 Email" clearable></el-input>
        </el-form-item>
        <el-form-item label="密码">
          <el-input v-model="loginForm.password" placeholder="请输入密码" show-password clearable></el-input>
        </el-form-item>
        <el-form-item>
          <a class="toCheckNum" href="#">手机验证码登陆</a>
          <a href="#" style="margin-left:90px" @click="to()">忘记密码?</a>
        </el-form-item>
        <el-form-item>
          <el-button class="toLogin" type="primary" @click="submitForm('loginForm')">登录</el-button>
          <i class="el-icon-d-arrow-right to" @click="toRegister()">去注册</i>
          <!-- <el-button type="" @click="resetForm('loginForm')">重置</el-button> -->
        </el-form-item>
        <!-- <el-form-item>
          <div class="aa">去注册</div>
        </el-form-item> -->
      </el-form>
      <el-form :model="registerForm" :rules="rules2" ref="registerForm" label-width="100px" id="registerForm">
        <el-form-item label="账号">
          <el-input v-model="registerForm.ID" placeholder="11位手机号 或 Email" clearable></el-input>
        </el-form-item>
        <el-form-item label="密码1" prop="passWord">
          <el-input v-model="registerForm.passWord" placeholder="请输入密码" show-password clearable autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item label="密码2" prop="checkPass">
          <el-input v-model="registerForm.checkPass" placeholder="请输入密码" show-password clearable  autocomplete="off"></el-input>
        </el-form-item>
        <el-form-item>
          <a class="toCheckNum" href="#">手机验证码注册</a>
        </el-form-item>
        <el-form-item>
          <i class="el-icon-d-arrow-right to left" @click="toLogin()">去登录</i>
          <el-button class="toLogin" type="primary" @click="submitForm('registerForm')">注册</el-button>
          <!-- <el-button type="" @click="resetForm('registerForm')">重置</el-button> -->
        </el-form-item>
      </el-form>
    </div>
  </div>
</template>
<script src="https://cdn.bootcss.com/jquery/3.3.1/jquery.js"></script>
<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    @import "../css/common.css";
    .redius{
        border-top-left-radius: 5px;
        border-top-right-radius: 5px;
    }
    .toLogin{
        width: 250px;
        color: #60809f;
        background: #dde8f4;
        border-color: #86a4c3;
    }
    .toLogin:focus , .toLogin:hover{
        background: #60809f;
        border-color: #60809f;
        color: #fff;
    }
    .showImg{
        height: 56%;
    }
    .hello{
        background-color: #fafafa;
        background-position: 50% 50%;
        width: 100%;
        height: 900px;
        padding: 100px;
    }
    #loginForm {
        padding: 20px;
    }
    .main{
        box-shadow: 0 2px 4px rgba(0, 0, 0, .12), 0 0 6px rgba(0, 0, 0, .04);
        background:rgba(255, 255, 255, 0.7);
        width: 500px;
        border-radius: 5px;
        margin: 0 auto;
    }
    .el-form-item{
        margin-bottom: 10px;
    }
    .el-input{
        width: 70%;
    }
    .toCheckNum{
        text-decoration: none;
    }
    .to{
        float: right;
        height: 40px;
        line-height: 40px;
        font-size: 16px;
        color: #60809f;
    }
    .to:hover{
        font-size: 17px;
        cursor: pointer;
    }
    #registerForm{
        display: none;
        padding: 20px;
    }
    /* .aa{
        width: 60px;
        height: 60px;
        border-radius: 50%;
        border: 2px solid #60809f;
        text-align: center;
        line-height: 50px;
        float: right;
    } */
</style>
<script>
  export default {
    data() {
      var validatePass = (rule, value, callback) => {
        if (value === '') {
          callback(new Error('请输入密码'));
        } else {
          if (this.registerForm.checkPass !== '') {
            this.$refs.registerForm.validateField('checkPass');
          }
          callback();
        }
      };
      var validatePass2 = (rule, value, callback) => {
        if (value === '') {
          callback(new Error('请再次输入密码'));
        } else if (value !== this.registerForm.passWord) {
          callback(new Error('两次输入密码不一致!'));
        } else {
          callback();
        }
      };
      return {
        loginForm: {
          ID: '',
          passWord: '',
        },
        registerForm: {
          ID:'',
          passWord: '',
          checkPass: ''
        },
        rules1: {
          ID: [
            { required: true, message: '请输入用户名', trigger: 'blur' },
            { min: 8, max: 20, message: '长度在 8 到 20 个字符', trigger: 'blur' }
          ],
          password: [
            { required: true, message: '请输入密码', trigger: 'change' }
          ]
        },
        rules2: {
          ID: [
            { required: true, message: '请输入用户名', trigger: 'blur' },
            { min: 8, max: 20, message: '长度在 8 到 20 个字符', trigger: 'blur' }
          ],
          password: [
            { required: true, message: '请输入密码', trigger: 'change' }
          ]
        }
      };
    },
    methods: {
      // 提交登录表单
      submitForm(formName) {
        this.$refs[formName].validate((valid) => {
          if (valid) {
              this.$router.push({path: '/Setting'});
            //   在新的页面打开
            // let routeData = this.$router.resolve({ path: '/Setting'});
            // window.open(routeData.href, '_blank');  
          } else {
            console.log('error submit!!');
            return false;
          }
        });
      },
      
      // 重置登录表单
      resetForm(formName) {
        this.$refs[formName].resetFields();
      },

      // 切换到注册页面
      toRegister(){
        // alert("去注册");
        var loginForm = document.getElementById('loginForm');
        var registerForm = document.getElementById('registerForm');
        loginForm.style.display='none';
        registerForm.style.display='block';
      },

      // 切换到登录页面
      toLogin(){
        // alert("去登录");
        var loginForm = document.getElementById('loginForm');
        var registerForm = document.getElementById('registerForm');
        loginForm.style.display='block';
        registerForm.style.display='none';
      }
    }
  }
</script>
