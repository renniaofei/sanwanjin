<template>
    <div class="login">
        <div class="login-content">
            <h2>三万金-注册</h2>
            <el-input class="reg-email" v-model="email" placeholder="请输入您的邮箱"></el-input>
            <el-input class="reg-code" v-model="code" placeholder="请输入您的邀请码"></el-input>
            <el-input class="reg-password" type='password' v-model="password" placeholder="请输入密码"></el-input>
          <el-input class="reg-password" type='password' v-model="password" placeholder="请确认密码"></el-input>
            <el-button type="primary" style="width:100%">注册</el-button>
              <br>
            <el-button style="width:100%">登录</el-button>
        </div>
    </div>
</template>
<script>
export default {
     data(){
         return{
             email:"",
             code:'',
             password:'',
         }
    }
}
</script>

<style scoped>
.login-content{
    width: 400px;
   margin: 100px auto 0;
}
.login-content button,.reg-email,.reg-code,.reg-password{
    margin-bottom: 20px;
}
</style>
