<template>
  <div class="menu">
    <el-menu  :default-active="activeIndex" class="el-menu-demo" mode="horizontal">
  <el-menu-item index="1">首页</el-menu-item>
   <el-menu-item index="2">帮助</el-menu-item>
    <el-menu-item index="3">充值</el-menu-item>
     <el-menu-item index="4">邀请</el-menu-item>
     <el-menu-item index="5">客服</el-menu-item>
  <el-menu-item index="3" disabled>消息中心</el-menu-item>
</el-menu>
  </div>
</template>
<script>
import { NavMenu } from "element-ui";
export default {
  name: "menu",
  data() {
    return {
      activeIndex: "1",
      activeIndex2: "1"
    };
  },
  components: { NavMenu },
  methods: {
    handleSelect(key, keyPath) {
      console.log(key, keyPath);
    }
  }
};
</script>

<style scoped>
</style>
