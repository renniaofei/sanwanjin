<template>
    <div class="index"  ref="index">
      <div class="particle" ref="particle"></div>
      
        <my-menu ></my-menu>
        <div class="index-content">
        <div class="downInput">
      <el-alert
    title="三万金©平台目前支持包图网，千库网，千图网，90设计"
    type="success"
    :closable="false">
  </el-alert>
    <br>
        <!-- <el-alert
            title="警告提示的文案警告提示的文案警告提示的文案警告提示的文案警告提示的文案"
            type="warning">
        </el-alert>
        <br> -->
        <el-input v-model="input" class="fl el-input" placeholder="请输入下载链接"></el-input>  <el-button class="fl" type="primary">点击下载</el-button>
        </div>
        </div>
    </div>
</template>
<script>
import myMenu from "@/components/myMenu";
  import Particle from 'zhihu-particle';
   
export default {
  data() {
    return {
      data: "1231",
      input: ""
    };
  },
  components: { myMenu },
  mounted() {
  //  var particle =   new Particle(this.$refs.particle);
  //  particle.option.interactive = true;
  },
};
</script>
<style scoped>
.particle{
  position: absolute;
  top: 61px;
  bottom: 0;
  left: 0;
  right: 0;
  overflow: hidden;
}
.menu ul{
  width: 1000px;
}
.index-content{
  position: absolute;
  top: 61px;
  left: 0;
  right: 0;
  bottom: 0;
  z-index: 20;
  width: 1000px;

  margin: 0 auto;
}
.downInput {
  margin-top: 40px;
}
.fl {
  float: left;
}
.el-input {
  width: 500px;
  margin-right: 20px;
}
</style>
