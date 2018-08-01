<template>
  <div class="myMenu">
    <ul>
      <li>首页</li>
      <li>帮助</li>
      <li>充值</li>
      <li>邀请</li>
      <li>客服</li>
    </ul>
     <div class="userName">
    <span class="">
     欢迎您 {{userInfoDatas.userId}}
    </span>
    <span class="logout" @click="logout">退出</span>
     </div>

   
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
  width: 1000px;
  margin: 0 auto;
  /* border:1px solid #e6e6e6;
  background: #fff; */
}
.myMenu ul li{
  height: 30px;
  line-height: 30px;
  float: left;
  margin-left: 10px;
  color: #fff;
}
.myMenu ul{
  float: left;
}
.logout{
  margin-left: 5px;
  color:red;
}
.userName{
  float: right;
  color: #fff ;
  cursor: pointer;
}
.menu-content{
    position: relative;
  width: 1000px;
  margin:0 auto;
}
</style>
