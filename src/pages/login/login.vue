<template>
    <div class="login">
        <div class="login-content">
            <h2>三万金-登录</h2>
            <el-input v-model="account" class="account" placeholder="请输入账号"></el-input>
            <el-input v-model="password" type='password' class="password" placeholder="请输入密码"></el-input>
            <el-button type="primary" class="login-btn" style="width:100%">登录</el-button>
            <br>
            <el-button style="width:100%">注册</el-button>
        </div>
    </div>
</template>
<script>
export default {
    data(){
        return{
            account:'',
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
.account,.password,.login-btn{
margin-bottom: 20px;
}    

</style>
