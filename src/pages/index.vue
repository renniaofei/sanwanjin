<template>
    <div class="index"  ref="index">
     
        <my-menu :userInfoDatas='userInfoDatas'></my-menu>
        <div class="index-content">
        <div class="downInput">
      <el-alert
    title="三万金©平台目前支持包图网"
    type="success"
    :closable="false">
  </el-alert>
    <br>
        <!-- <el-alert
            title="警告提示的文案警告提示的文案警告提示的文案警告提示的文案警告提示的文案"
            type="warning">
        </el-alert>
        <br> -->
        <el-input v-model="downInput" class="fl el-input"   placeholder="请输入下载链接"></el-input>  <el-button class="fl"  @click="getDownInfo" :loading="false"  type="primary">点击下载</el-button>
        </div>
        <div class="downInfo-wrap" v-if="downInfo.title">
          <div class="download-wrap"><el-button @click="download"  :loading="false" type="success">VIP高速下载</el-button></div>
         <p class="title"><span>标题：</span>{{downInfo.title}}</p> 
          </div>
        </div>
    </div>
</template>
<script>
import myMenu from "@/components/myMenu";
import {userInfo,btwDownInfo,btwDownLoad} from "@/api/index"
import {getCookie} from "@/untils/untils"
  // import Particle from 'zhihu-particle';
   
export default {
  data() {
    return {
      data: "1231",
      downInput: "",
      downInfo:{
        title:''
      },
      userInfoDatas:{},
      webId:'',
    };
  },
  components: { myMenu },
  mounted() {
    this.isLogin()
  },

  methods:{
    download(){
      this.openFullScreen()
      let params = {
        'webId':this.webId
      }
      console.log(params);
      btwDownLoad(params).then(res=>{
        // console.log(res);
        if(res.code==100)
        {
          window.location.href = res.data;
        }
        else{
            this.$message.error("下载失败，请稍后再试！");
        }
      })
    },
    getDownInfo(){
      
      var downUrl = this.downInput;
      let reg = /(ibaotu|588ku).com/g
      if(reg.test(downUrl))
      {
        this.openFullScreen();
          this.webId = this.getWebId(downUrl);
          let params ={
            'webId': this.getWebId(downUrl)
          }
          btwDownInfo(params).then(res =>{

            this.downInfo.title = res.data.title;

          })
      }
      else{
          this.$message.error("抱歉你输入的网站暂不支持！");
      }
    },
    getWebId(downUrl){
      let startIndex = downUrl.lastIndexOf('/')+1;
      let endIndex = downUrl.lastIndexOf('.');
      return downUrl.substring(startIndex,endIndex)
      
    },
    isLogin(){
      let token =  getCookie("token");
      // console.log(token);
      var that = this;
      if(token)
      {
      let params = {
        'token':getCookie('token')
      }
      userInfo(params).then(res=>{
        //  console.log(res,'返回的用户数据');
        if(res.code === 100)
        {
          that.userInfoDatas = res.data;
          console.log(this.userInfoDatas,'返回的用户数据');
        }
        else{
          this.$router.push('/login')
        }
      }).catch(err=>{
       this.$router.push('/login')
      })
      }
      else{
        this.$router.push('/login')
      }
    },
      openFullScreen() {
        const loading = this.$loading({
          lock: true,
          text: 'Loading',
          spinner: 'el-icon-loading',
          background: 'rgba(0, 0, 0, 0.7)'
        });
        setTimeout(() => {
          loading.close();
        }, 1000);
      }
    }
  
};
</script>
<style scoped>
.download-wrap{
  text-align: left;
}
.downInfo-wrap{
  text-align: left;
}

.menu ul{
  width: 1000px;
}
.index-content{
  height: 100%;
  width: 1000px;

  margin: 61PX auto;
}
.downInput {
  margin-top: 40px;
  height: 120px;
}
.fl {
  float: left;
}
.el-input {
  width: 500px;
  margin-right: 20px;
}
</style>
