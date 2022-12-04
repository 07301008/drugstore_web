<template>
  <el-menu
      background-color="#545c64"
      text-color="#fff"
      active-text-color="#ffd04b"
      default-active="/Home"
      style="height: 100vh;">
    <el-menu-item index="/Home">
      <i class="el-icon-s-home"></i>
      <span>员工管理</span>
    </el-menu-item>
    <el-menu-item index="/One">
      <i class="el-icon-s-home"></i>
      <span>导航一</span>
    </el-menu-item>
    <el-menu-item index="/Two">
      <i class="el-icon-s-home"></i>
      <span>导航二</span>
    </el-menu-item>
  </el-menu>
</template>

<script>
export default {
  name: "Aside"
}
</script>

<style scoped>

</style>