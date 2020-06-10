<template>
  <div class="header">
    <!-- 导航内容 -->
    <el-breadcrumb separator="/">
      <el-breadcrumb-item
        :key="bread.title"
        v-for="bread in breadArr"
        :to="{ path: bread.path }"
        >{{ bread.title }}</el-breadcrumb-item
      >
    </el-breadcrumb>
    <!-- 右边 -->
    <div class="header-right">
      <!-- 下拉框 -->
      <el-dropdown @command="handleCommand">
        <span class="el-dropdown-link">
          欢迎你，{{acc}}
          <i class="el-icon-arrow-down el-icon--right"></i>
        </span>
        <el-dropdown-menu slot="dropdown">
          <el-dropdown-item command="personal">个人中心</el-dropdown-item>
          <el-dropdown-item command="logout">退出系统</el-dropdown-item>
        </el-dropdown-menu>
      </el-dropdown>
      <!-- 头像 -->
      <el-avatar v-if="imgUrl" :size="size" :src="avatarServeUrl + imgUrl"></el-avatar>
    </div>
  </div>
</template>

<script>
// 引入工具函数
import local from "@/utils/local";
// 引入获取信息函数
import { getuserInfo } from "@/api/account";
export default {
  data() {
    return {
      size: 50,
      acc: "",
      imgUrl: "",
      avatarServeUrl: "http://127.0.0.1:5000/upload/account/", //头像图地址
      // 面包屑
      breadArr: [],
    };
  },
  methods: {
    // 下拉框点击事件
    handleCommand(command) {
      if (command === "logout") {
        // 退出系统就删除token
        local.remove("t_k");
        this.$message({
          type: "success",
          message: "要记得回来哦"
        });
        // 跳转到登录页面
        this.$router.push("/");
      } else {
        // 跳转到个人中心
        this.$router.push("/index/personal");
      }
    },
    // 获取数据
    async getAccAndAvatar() {
      let {accountInfo} = await getuserInfo(); // 发送请求获取数据
      // console.log(typeof accountinfo);
      this.acc = accountInfo.account; // 赋值给账号
      this.imgUrl = accountInfo.imgUrl; // 赋值给头像
    },
     // 计算面包屑
    calcBread() {
      // 算出面包屑
      this.breadArr = [
        { path: "/index", title: "首页" },
        this.$route.meta.bread,
      ];
    },
  },
 
  // 生命周期
  created() {
    this.getAccAndAvatar();
    // 接受个人中心的通知
    this.$bus.$on("gxtx",()=>{
      // 重新获取下一条数据
      this.getAccAndAvatar();
    });
     // 计算面包屑
    this.calcBread();
  },
  // 侦听器
  watch: {
    // 观察路由地址变化
    "$route.path"() {
      // 计算面包屑
      this.calcBread();
    },
  },
};
</script>

<style lang="less" scoped>
.header {
  background: #fff;
  flex: 0 0 40px;
  display: flex;
  justify-content: space-between;
  .el-breadcrumb__item {
    line-height: 40px;
    margin-left: 20px;
    // justify-self: start;
  }
  .el-avatar {
    margin-right: 20px;
  }
  .header-right {
    display: flex;
    align-items: center;
    .el-dropdown {
      margin-right: 10px;
    }
  }
  /deep/ .el-dropdown-item {
    a {
      text-decoration: none;
      color: #000;
    }
  }
}
</style>