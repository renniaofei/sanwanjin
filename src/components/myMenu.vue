<template>
  <div class="myMenu clearfix">
    <ul class="clearfix">
      <li>首页</li>
      <li @click="helper">帮助</li>
      <li @click="buy">购买</li>
      <!-- <li>邀请</li> -->
      <li @click="openKefu">客服</li>
    </ul>
     <div class="userName ">
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
      weixinKefu:require('../pages/img/weixin.jpg')
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
       openKefu() {
        this.$alert(' <img style="width:200px;height:200px" src='+this.weixinKefu+'/>', '客服微信', {
          dangerouslyUseHTMLString: true
        });
      },
      buy(){
        window.open("https://shop68949178.taobao.com/shop/view_shop.htm?spm=a1z09.1.category.d53.44543606Q6MXTo&mytmenu=mdianpu&user_number_id=692494543","_blank");         

      },
       helper(){
        window.open('https://shimo.im/doc/0ythof1lhH0Qu9Rj','_blank')
        // this.$router.push("https://shimo.im/doc/0ythof1lhH0Qu9Rj")
      },
  }
};
</script>

<style scoped>
.myMenu{
  width: 1000px;
  margin: 0 auto;
  height: 50px;
  line-height: 50px;
  /* border:1px solid #e6e6e6;
  background: #fff; */
}
.myMenu ul li{
  height: 50px;
  line-height: 50px;
  float: left;
  margin-right: 30px;
  color: #fff;
  /* font-size: 14px; */
  cursor: pointer;
}
.myMenu ul{
  float: left;
}
.logout{
  margin-left: 5px;
  color:floralwhite;
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
