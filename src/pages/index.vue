<template>
    <div class="index"  ref="index">
        <my-menu :userInfoDatas='userInfoDatas'></my-menu>
        <div class="index-content">
        <div class="downInput">
      <div class="userInfro">
          <ul>
            <li v-if="userInfoDatas.btw==1"><span>网站：<strong>包图网</strong></span><span></span><span>已使用：<strong>{{userInfoDatas.btwNums}}/共{{btwType}}</strong></span><span>到期时间：<strong>{{vipDeadline('btw')}}</strong></span></li>
            <li v-if="userInfoDatas.qkw==1"><span>网站：<strong>千库网</strong></span><span></span><span>已使用：<strong>{{userInfoDatas.qkwNums}}/共{{userInfoDatas.qkwType}}</strong></span><span>到期时间：<strong>{{vipDeadline('qkw')}}</strong></span></li>
          </ul>
        </div>
        <el-input v-model="downInput" class="fl el-input"  style="width:600px;height:50px"  placeholder="请输入下载链接"></el-input>  <el-button class="fl"  @click="getDownInfo" :loading="false"  type="primary">点击下载</el-button>
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
import { userInfo, DownInfo, DownLoad } from "@/api/index";
import { getCookie, GMTToStr } from "@/untils/untils";

export default {
  data() {
    return {
      data: "1231",
      downInput: "",
      downInfo: {
        title: ""
      },
      fullscreenLoading: false,
      userInfoDatas: {},
      webId: ""
    };
  },
  computed: {
    btwType() {
      switch (this.userInfoDatas.btwType) {
        case "c":
          return "5";
          break;
        case "z":
          return "10";
          break;
        default:
          break;
      }
    }
  },
  components: { myMenu },
  mounted() {
    this.isLogin();
  },
  methods: {
    vipDeadline(webType) {
      if (webType == "btw") {
        return GMTToStr(this.userInfoDatas.btwDeadline);
      } else if (webType == "qkw") {
        return GMTToStr(this.userInfoDatas.qkwDeadline);
      }
    },
    _download(downUrl) {
      let params = {
        downUrl: downUrl
      };
      DownInfo(params).then(res => {
        if (res.code == 200) {
          console.log(res.data.title);
          this.downInfo.title = res.data.title;
        } else if (res.code == "300") {
          this.$message.error("你输入的网站暂不支持！");
        } else if (res.code == "401") {
          this.$message.error("未查询到该素材！");
        } else if (res.code == "500") {
          this.$message.error("查询下载素材信息-系统错误!");
        }
      });
    },
    download() {
      this.openFullScreen();
      let params = {
        webId: this.webId
      };
      console.log(params);
      btwDownLoad(params).then(res => {
        // console.log(res);
        if (res.code == 100) {
          window.location.href = res.data;
        } else {
          this.$message.error("下载失败，请稍后再试！");
        }
      });
    },
    getDownInfo() {
      var downUrl = this.downInput;
      let reg = /(ibaotu|588ku).com/g;
      if (reg.test(downUrl)) {
        let webType = this.getwebType(downUrl);
        if (webType == "ibaotu") {
          if (this.userInfoDatas.btw == 1) {
            this._download(downUrl);
          } else {
            this.$message.error("你未开通包图网");
          }
        } else if (webType == "588ku") {
          if (this.userInfoDatas.qkw == 1) {
            this._download(downUrl);
          } else {
            this.$message.error("你未开通千库网");
          }
        }
        // this.webId = this.getWebId(downUrl);
      } else {
        this.$message.error("你输入的网站暂不支持！");
      }
    },
    getWebId(downUrl) {
      let startIndex = downUrl.lastIndexOf("/") + 1;
      let endIndex = downUrl.lastIndexOf(".");
      return downUrl.substring(startIndex, endIndex);
    },
    checkVip(){
      if(this.userInfoDatas.btw==1)
      {}
    },
    getwebType(downUrl) {
      let webType = downUrl.substring(
        downUrl.indexOf("//") + 2,
        downUrl.indexOf(".")
      );
      console.log(webType);
      return webType;
    },
    isLogin() {
      let token = getCookie("token");
      var that = this;
      if (token) {
        let params = {
          token: getCookie("token")
        };
        userInfo(params)
          .then(res => {
            console.log(res, "返回用户数据");
            if (res.total == 1 && res.code == 200) {
              that.userInfoDatas = res.rows[0];
              console.log(that.userInfoDatas, "200返回的用户数据");
            } else {
              this.$router.push("/login");
            }
          })
          .catch(err => {
            this.$router.push("/login");
          });
      } else {
        this.$router.push("/login");
      }
    },
    openFullScreen() {
      this.fullscreenLoading = true;
      setTimeout(() => {
        this.fullscreenLoading = false;
      }, 1000);
    }
  }
};
</script>
<style scoped>
.title {
  color: #fff;
}
.download-wrap {
  text-align: left;
}
.downInfo-wrap {
  text-align: left;
}
.userInfro ul li span {
  margin-right: 20px;
  font-size: 14px;
  color: #fff;
}
.userInfro ul li {
  text-align: left;
  color: #fff;
  margin-bottom: 10px;
}
.menu ul {
  width: 1000px;
}
.index-content {
  height: 100%;
  width: 1000px;

  margin: 61px auto;
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
