<template>
  <div style="display: flex;line-height: 60px;">
    <div style="flex: 1;text-align: center;font-size: 20px;">
      <span>欢迎来到药店管理系统</span>
    </div>
    <span>王小虎</span><i style="margin-left: 5px"></i>
    <el-dropdown>
      <i class="el-icon-arrow-down" style="margin-right: 15px;"></i>
      <el-dropdown-menu slot="dropdown">
        <el-dropdown-item>个人中心</el-dropdown-item>
        <el-dropdown-item @click.native="logout">退出登录</el-dropdown-item>
      </el-dropdown-menu>
    </el-dropdown>
  </div>
</template>

<script>
export default {
  name: "Header",
  methods:{
    // 退出登录
    logout(){
      console.log('logout')
    }
  }
}
</script>

<style scoped>

</style>