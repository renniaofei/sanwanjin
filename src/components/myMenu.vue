<template>
  <div class="myMenu">
    <el-menu  :default-active="activeIndex" class="menu-content" mode="horizontal">
  <el-menu-item index="1">首页</el-menu-item>
   <el-menu-item index="2">帮助</el-menu-item>
    <el-menu-item index="3">充值</el-menu-item>
     <el-menu-item index="4">邀请</el-menu-item>
     <el-menu-item index="5">客服</el-menu-item>

</el-menu>
  </div>
</template>
<script>
import { NavMenu } from "element-ui";
export default {
  name: "myMenu",
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
.myMenu{
  border:1px solid #e6e6e6;
}
.menu-content{
  width: 1000px;
  margin:0 auto;
}
</style>
