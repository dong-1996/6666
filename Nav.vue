<template>
  <div class="Nav">
    <!-- 导航内容 -->
    <div class="logo">
      <img src="../../assets/images/logo.png" alt />
      <span>外卖商家中心</span>
    </div>
    <el-menu
      router
      unique-opened
      class="left-nav"
      background-color="#052a44"
      text-color="#fff"
      :default-active="$route.path"
    >
      <!-- 多级的 -->
      <!-- 后台首页 -->
      <el-menu-item index="/index/home">
        <i class="iconfont icon-shouye"></i>
        <span slot="title">后台首页</span>
      </el-menu-item>
      <!-- 订单管理 -->
      <el-menu-item index="/index/order">
        <i class="iconfont icon-dingdan"></i>
        <span slot="title">订单管理</span>
      </el-menu-item>
      <!-- 商品管理 -->
      <el-submenu index="商品管理">
        <template slot="title">
          <i class="iconfont icon-shangpin"></i>
          <span>商品管理</span>
        </template>
        <el-menu-item index="/index/goodslist">商品列表</el-menu-item>
        <el-menu-item index="/index/goodsadd">添加商品</el-menu-item>
      </el-submenu>
      <!-- 店铺管理 -->
      <el-menu-item index="/index/shop">
        <i class="iconfont icon-dianpu"></i>
        <span slot="title">店铺管理</span>
      </el-menu-item>
      <!-- 账号管理 -->
      <el-submenu index="/index/accountlist">
        <template slot="title">
          <i class="iconfont icon-zhanghao"></i>
          <span>账号管理</span>
        </template>
        <el-menu-item index="/index/accountlist">账号列表</el-menu-item>
        <el-menu-item index="/index/accountadd">添加账号</el-menu-item>
        <el-menu-item index="/index/modifypass">修改密码</el-menu-item>
      </el-submenu>
      <!-- 销售统计 -->
      <el-submenu index="6">
        <template slot="title">
          <i class="iconfont icon-tongji"></i>
          <span>销售统计</span>
        </template>
        <el-menu-item index="/index/goodstotal">商品统计</el-menu-item>
        <el-menu-item index="/index/ordertotal">订单统计</el-menu-item>
      </el-submenu>
    </el-menu>
  </div>
</template>

<script>
export default {};
</script>

<style lang="less" scoped>
.Nav {
  flex: 0 0 200px;
  background: #052a44;
  .logo {
    height: 50px;
    display: flex;
    justify-content: center;
    align-items: center;
    img{
      height: 40px;
      line-height: 40px;
    }
    span{
      line-height: 40px;
      margin-left: 10px;
      color: #eee;
      font-weight: 500;
    }
  }
  .el-menu{
    border-right: 0px;
    .iconfont{
      margin-right: 10px;
      color: #E6A23C;
    }
  }
  .el-submenu {
    /deep/.el-menu {
      .el-menu-item {
        background-color: #042236 !important;
      }
    }
  }
}
</style>