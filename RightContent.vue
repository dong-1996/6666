<template>
  <div class="Right-Content">
    <!-- 顶部导航 -->
    <Header />
    <!-- 内容 -->
 <div class="content">
    <router-view />
 </div>
  </div>
</template>

<script>
// 引入路由
import Header from "@/components/Layout/Header.vue"
export default {
  components:{
    Header
  }
};
</script>

<style lang="less" scoped>
.Right-Content {
  flex: 1;
  background: #eee;
  flex-direction: column;
  display: flex;
  .content{
    flex: 1;
  }
}
</style>