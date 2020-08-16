<template>
  <el-collapse v-loading="loading">
    <el-collapse-item v-for="t in tasks" :key="t.id" :title="t.name">
      <Task :task="t" :time="[t.startdt,t.overdt]"></Task>
    </el-collapse-item>
  </el-collapse>
</template>
<script>
import Task from "./Task.vue";
export default {
  name: "TaskList",
  components: {
    Task,
  },
  data() {
    return {
      tasks: {},
      tasksnum: { "2020-8-16": 2 },
      loading: true,
    };
  },
  created: function () {
    console.log(this.tasksnum["2020-8-16"]);
    this.$axios
      .get("http://pi.deadpoetspoon.xyz:7900/tasks/?format=json")
      .then((response) => {
        var data = this;
        //console.log(response.data);
        response.data.forEach((task) => {
          console.log(typeof task.startdt);
        });
        data.tasks = response.data;
        this.loading = false;
      })
      .catch((error) => {
        // 请求失败处理
        console.log(error);
        this.$message({
          showClose: true,
          message: error,
          type: "error",
        });
      });
  },
};
</script>
<style>
</style>
