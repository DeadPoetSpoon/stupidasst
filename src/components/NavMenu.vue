<template>
  <div id="app">
    <el-menu default-active="1-4-1" class="el-menu-vertical-demo" @select="handleSelect" :collapse="isCollapse">
      <el-tooltip :content="menutip" placement="top" class="el-menu-switch">
        <el-switch v-model="isCollapse" value="isCollapse"  active-color='#13ce66' inactive-color='#ff4949' ></el-switch>
      </el-tooltip>
      <el-menu-item index="1" selected>
        <i class="el-icon-menu"></i>
        <span slot="title">快捷链接</span>
      </el-menu-item>
      <el-menu-item index="2">
        <i class="el-icon-date"></i>
        <span slot="title">任务清单</span>
      </el-menu-item>
      <el-menu-item index="3">
         <i class="el-icon-s-custom"></i>
         <span slot="title">管理界面</span>
       </el-menu-item>
    </el-menu>
  </div>
</template>
<script>
export default{
  name: 'NavMenu',
  data() {
    return {
      isCollapse: true,
      menutip: "菜单开关"
    };
  },
  methods:{
    handleSelect(index,indexPath){
      console.log(index,indexPath);
      var com = "";
      if(index == 1){
        com = "LinkPanel";
      } else if(index == 2){
        com = "TaskList";
      } else if(index == 3){
        com = "Admin";
      }
      this.$emit('select',com);     
    }
  }
}
</script>
<style>
.el-menu-vertical-demo:not(.el-menu--collapse) {
  width: 150px;
  min-height: 400px;
}
</style>
