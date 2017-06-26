<template>
<div  class="sidebar">

    <el-menu class="el-menu-vertical-demo" default-active="onRoutes"  @open="handleOpen" @close="handleClose" theme="dark" unique-opened router>

<el-menu-item index="basetable">导航菜单</el-menu-item>
<el-menu-item index="vuetable">IOMAT</el-menu-item>
<el-menu-item index="baseform">用户管理</el-menu-item>
<el-menu-item index="vueeditor">企业机器人管理</el-menu-item>
<template>
      <el-submenu index="5">
          <template slot="title" index="5-0">财务管理</template>
          <el-menu-item index="upload" ><i class="el-icon-star-on"></i>交易中心</el-menu-item>
          <el-menu-item index="markdown"><i class="el-icon-star-on"></i>提现管理</el-menu-item>
      </el-submenu>
</template>

<el-menu-item index="basecharts">朋友圈管理</el-menu-item>
<el-menu-item index="drag">AI直播管理</el-menu-item>
     
</el-menu>

</div>
</template>
<script>
  export default {
    methods: {
      handleOpen(key, keyPath) {
        console.log(key, keyPath);
      },
      handleClose(key, keyPath) {
        console.log(key, keyPath);
      },
      jyzx(){

      },
      computed:{
            onRoutes(){
                return this.$route.path.replace('/','');
            }
        }
    }
  }
</script>

<style scoped>
    .sidebar{
        display: block;
        position: absolute;
        width: 250px;
        left: 0;
        top: 70px;
        bottom:0;
        background: #2E363F;
    }
    .sidebar > ul {
        height:100%;
    }
</style>
