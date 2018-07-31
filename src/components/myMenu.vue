<template>
  <div class="myMenu">
    <el-menu  :default-active="activeIndex"  class="menu-content" mode="horizontal">
  <el-menu-item index="1">首页</el-menu-item>
   <el-menu-item index="2" >帮助</el-menu-item>
    <el-menu-item index="3">充值</el-menu-item>
     <el-menu-item index="4">邀请</el-menu-item>
     <el-menu-item index="5">客服</el-menu-item>
     <div class="userName">
    <span class="">
     欢迎您 {{userInfoDatas.userId}}
    </span>
    <span class="logout" @click="logout">退出</span>
     </div>
</el-menu>
   
  </div>
</template>
<script>
import { NavMenu } from "element-ui";
import {delCookie} from "@/untils/untils"
export default {
  name: "myMenu",
  data() {
    return {
      activeIndex: "1",
      activeIndex2: "1",

    };
  },
  mounted() {
    console.log('datas',this.userInfoDatas);
  },
  props:{
    userInfoDatas:{
      type:Object,
      default:{},
    }
  }
    
  ,
  components: { NavMenu },
  methods: {
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
    },
    logout(){
      delCookie('token');
      this.$router.push('/login')
    },
  }
};
</script>

<style scoped>
.myMenu{
  border:1px solid #e6e6e6;
  background: #fff;
}
.logout{
  margin-left: 5px;
  color:red;
}
.userName{
  position: absolute;
  right: 10px;
  top: 20px;
  cursor: pointer;
}
.menu-content{
   position: relative;
  width: 1000px;
  margin:0 auto;
}
</style>
