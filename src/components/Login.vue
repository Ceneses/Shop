<template>
    <div id="login" class="login_container">
      <div class="login_box">
        <div class="avatar_box">
          <img src="../assets/man.jpeg" alt="图片没找到">
        </div>
        <el-form ref="loginFormRef" class="form_box" :rules="rules" label-suffix=" :" label-width="80px" :model="login_form">
            <el-form-item label="用户名" prop="username">
              <el-input prefix-icon="el-icon-user" v-model="login_form.username"></el-input>
            </el-form-item>
            <el-form-item label="密码" prop="password">
              <el-input prefix-icon="el-icon-lock" v-model="login_form.password" type="password"></el-input>
            </el-form-item>
            <el-form-item>
              <el-link type="primary">忘记密码</el-link>
              <div style="display: inline-block; position: absolute; right: 0px">
                <el-button type="primary" @click="loginForm">登录</el-button>
                <el-button @click="resetLoginForm">重置</el-button>
              </div>
            </el-form-item>
          </el-form>
      </div>
    </div>
</template>

<script>
  export default {
    name: 'Login',
    data () {
      return {
        login_form: {
          username: 'admin',
          password: '123456'
        },
        rules: {
          username: [
            { required: true, message: '请输入用户姓名', trigger: 'blur' },
            { min: 3, max: 5, message: '长度在 3 到 5 个字符', trigger: 'blur' }
          ],
          password: [
            { required: true, message: '请输入用户密码', trigger: 'blur' },
            { min: 6, max: 15, message: '长度在 6 到 15 个字符', trigger: 'blur' }
          ]
        }
      };
    },
    methods: {
      loginForm () {
        this.$refs.loginFormRef.validate(async valid => {
          if (!valid) return;
          const { data: res } = await this.$http.post('login', this.login_form);
          if (res.meta.status === 200) {
            this.$message({
              showClose: true,
              message: '登陆成功',
              type: 'success'
            });
          }
        });
      },
      resetLoginForm () {
        this.$refs.loginFormRef.resetFields();
      }
    }
  };
</script>

<style lang="less" scoped>
  .login_container{
    background-color: #6eb6ff;
    height: 100%;
  }
  .login_box{
    width: 600px;
    height: 500px;
    background-color: #FFFFFF;
    border-radius: 10%;
    position: absolute;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
  }
  .avatar_box{
    height: 200px;
    width: 200px;
    border: 1px solid #eeeeee;
    border-radius: 50%;
    padding: 10px;
    box-shadow: 0 0 10px #dddddd;
    position: absolute;
    left: 50%;
    transform: translate(-50%,-50%);
    background-color: #FFFFFF;
    img{
      width: 100%;
      height: 100%;
      border-radius: 50%;
      background-color: #eeeeee;
    }
  }
  .form_box{
    width: 100%;
    position: absolute;
    bottom: 100px;
    padding: 0 50px;
    box-sizing: border-box;
  }
</style>
