<template>
  <div class="login">
    <el-form class="login-form">
      <h1 class="title">用户登录</h1>
      <el-form-item prop="username">
        <i class="iconfont icon-yonghu"></i>
        <el-input type="text" v-model="user.username" />
      </el-form-item>
      <el-form-item prop="password">
        <i class="iconfont icon-mima"></i>
        <el-input :type="look ? 'password' : 'text'" v-model="user.password" />
        <i
          @click="isLook()"
          :class="look ? 'iconfont icon-yanjing-bi' : 'iconfont icon-yanjing'"
        ></i>
      </el-form-item>
      <el-button type="primary" @click="regi">注册</el-button>
      <br />
      <h4> </h4>
      <el-button type="primary" @click="login">登录</el-button>
      
    </el-form>
  </div>
</template>

<script>
import { reqAPI } from '@/request';
export default {
  data() {
    return {
      // showLoading:false,
      look: true,
      user: {
        username: "admin",
        password: "123",
      },
    };
  },
  methods: {
    loading() {
      this.$root.$guser = this.user.username;
      const loading = this.$loading({
        lock: true,
        text: "正在登录请稍等...",
        spinner: "el-icon-loading",
        background: "rgba(0, 0, 0, 0.7)",
      });
      setTimeout(() => {
        loading.close();
        this.$router.push("/home");
      }, 500);
    },
    regi(){
      this.$router.push("/register");
    },
    login() {
      this.showLoading = true;
      var res = reqAPI('GET',`/login,${this.user.username},${this.user.password}`, null);
      if(res.can == true){
        this.loading();
        this.$root.$guserid = res.id;
      }
      else
        alert("用户名或密码错误");
    },
    isLook() {
      this.look = !this.look;
    },
  },
};
</script>

<style  scoped>
.login {
  width: 100%;
  height: 100%;
  background: rgb(45, 58, 75);
  color: #fff;
  display: flex;
  justify-content: center;
  align-content: space-around;
}
.login-form {
  margin-top: -15%;
  width: 450px;
  display: flex;
  justify-content: center;
  align-content: center;
  flex-direction: column;
}
.login >>> .el-input__inner {
  border: none;
  background: none;
  color: #fff;
  font-size: 20px;
}
.title {
  text-align: center;
  margin-bottom: 30px;
  font-size: 30px;
}
.login >>> .el-form-item__content {
  display: flex;
  justify-content: center;
  align-content: center;
  border: 2px solid rgb(63, 81, 104);
  border-radius: 5px;
  padding: 5px 15px;
}
</style>