<template>
    <div class="login">
        <div class="login-content">
            <h2>三万金-登录</h2>
            <el-input v-model="account" class="account" placeholder="请输入账号"></el-input>
            <el-input v-model="password" type='password' class="password" placeholder="请输入密码"></el-input>
            <el-button type="primary" class="login-btn" @click="login" style="width:100%">登录</el-button>
            <br>
            <el-button style="width:100%">注册</el-button>
        </div>
    </div>
</template>
<script>
import { userLogin } from "@/api/index"
import {setCookie} from "@/untils/untils";
export default {
  data() {
    return {
      account: "",
      password: ""
    };
  },
  mounted() {},
  methods: {
    login() {
      let params = {
        user: this.account,
        password: this.password
      };
      userLogin(params).then(res => {
        console.log('登录res',res)
        if (res.code == 200&&res.total==1) {
          setCookie('token',res.rows[0].token);
          this.$message({
            message: "登录成功",
            type: "success"
          });
          this.$router.push('/')
        } else if (res.total == 1&&res.rows[0].enabled=='4') {
          this.$message.error("账号被禁用");
        } else if (res.total == 0&&res.code==200) {
          this.$message.error("用户名或密码错误");
        }
        else{
          this.$message.error("登录错误，请联系客服！");
        }
      });
    }
  }
};
</script>

<style scoped>
.login-content {
  width: 400px;
  margin: 100px auto 0;
}

.account,
.password,
.login-btn {
  margin-bottom: 20px;
}
</style>
