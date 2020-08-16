<template>
  <div>
    <el-card shadow="never">
      <el-row :gutter="20">
        <el-col :span="8">{{task.name}}</el-col>
        <el-col :span="8">
          <el-date-picker
            v-model="time"
            type="datetimerange"
            range-separator="至"
            start-placeholder="开始日期"
            end-placeholder="结束日期"
            disabled="true"
          ></el-date-picker>
        </el-col>
        <el-col :span="8">
          <el-button type="text" @click="dialogVisible = true">查看更多</el-button>
        </el-col>
      </el-row>
    </el-card>
    <el-dialog :visible.sync="dialogVisible">
      <TaskForm :task="task"></TaskForm>
    </el-dialog>
  </div>
</template>
<script>
import TaskForm from "./TaskForm";
export default {
  name: "Task",
  props: ["task", "time"],
  components: {
    TaskForm,
  },
  data() {
    return {
      dialogVisible: false,
    };
  },
};
</script>