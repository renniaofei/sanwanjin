<template>
    <div class="index">
        <my-menu></my-menu>
        <div class="downInput">
      <el-alert
    title="三万金©平台目前支持包图网，千库网，千图网，90设计"
    type="success"
    :closable="false">
  </el-alert>
    <br>
        <el-alert
            title="警告提示的文案警告提示的文案警告提示的文案警告提示的文案警告提示的文案"
            type="warning">
        </el-alert>
        <br>
             <el-input v-model="input" class="fl el-input" placeholder="请输入下载链接"></el-input>  <el-button class="fl" type="primary">点击下载</el-button>
        </div>
    </div>
</template>
<script>
import myMenu from "@/components/menu";
export default {
  data() {
    return {
      data: "1231",
      input: ""
    };
  },
  components: { myMenu }
};
</script>
<style scoped>
.index {
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
