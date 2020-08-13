<template>
  <div>
    <el-calendar>
      <template
      v-slot:dateCell="{date, data}">
        <p>{{ data.day.split('-').slice(1).join('-') }}</p>
        <el-button type="text" @click="dialog = true">{{tasksnum[1]==0?'':tasksnum[1]}}</el-button>
        <el-dialog title="收货地址" :visible.sync="dialog">
          <el-form :model="form">
            <el-form-item label="活动名称" >
              <el-input v-model="form.name" autocomplete="off"></el-input>
            </el-form-item>
            <el-form-item label="活动区域" >
              <el-select v-model="form.region" placeholder="请选择活动区域">
              <el-option label="区域一" value="shanghai"></el-option>
              <el-option label="区域二" value="beijing"></el-option>
              </el-select>
            </el-form-item>
          </el-form>
          <div slot="footer" class="dialog-footer">
            <el-button type="primary" @click="dialog = false">返 回</el-button>
          </div>
        </el-dialog>
      </template>
    </el-calendar>
  </div>
</template>
<script>
export default{
  name:'TaskList',
  data(){
    return {
      dialog:false,
      form:{
        name:'test',
        region:'diqu'
      },
      tasksnum:[0,1,2]
    };
  }
}
</script>
<style>
</style>
