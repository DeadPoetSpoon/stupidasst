<template>
  <el-form label-position="right" label-width="80px" :model="task" size="mini" :inline="forminline">
    <el-form-item label="id">
      <el-input v-model="task.id"></el-input>
    </el-form-item>
    <el-form-item label="Name">
      <el-input v-model="task.name"></el-input>
    </el-form-item>
    <el-form-item label="Startdt">
      <el-date-picker
        v-model="task.startdt"
        type="datetime"
        placeholder="选择日期时间"
        align="right"
        :picker-options="pickerOptions"
      ></el-date-picker>
    </el-form-item>
    <el-form-item label="Overdt">
      <el-date-picker
        v-model="task.overdt"
        type="datetime"
        placeholder="选择日期时间"
        align="right"
        :picker-options="pickerOptions"
      ></el-date-picker>
    </el-form-item>
    <el-form-item label="Createdt">
      <el-date-picker
        v-model="task.createdt"
        type="datetime"
        placeholder="选择日期时间"
        align="right"
        :picker-options="pickerOptions"
      ></el-date-picker>
    </el-form-item>
    <el-form-item>
      <el-checkbox v-model="task.importance">Importance</el-checkbox>
    </el-form-item>
    <el-form-item>
      <el-checkbox v-model="task.finished">Finished</el-checkbox>
    </el-form-item>
    <el-form-item>
      <el-checkbox v-model="task.delay">Delay</el-checkbox>
    </el-form-item>
    <el-form-item label="Remarks">
      <el-input type="textarea" autosize placeholder="请输入内容" v-model="task.remarks"></el-input>
    </el-form-item>
    <el-form-item>
      <el-button type="primary" icon="el-icon-edit" circle @click="edittask"></el-button>
      <el-button type="danger" icon="el-icon-delete" circle @click="deletetask"></el-button>
      <el-button type="success" icon="el-icon-check" circle @click="createtask"></el-button>
    </el-form-item>
  </el-form>
</template>
<script>
export default {
  name: "TaskForm",
  props: ["task"],
  data() {
    return {
      forminline:true,
      pickerOptions: {
        shortcuts: [
          {
            text: "今天",
            onClick(picker) {
              picker.$emit("pick", new Date());
            },
          },
          {
            text: "昨天",
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24);
              picker.$emit("pick", date);
            },
          },
          {
            text: "一周前",
            onClick(picker) {
              const date = new Date();
              date.setTime(date.getTime() - 3600 * 1000 * 24 * 7);
              picker.$emit("pick", date);
            },
          },
        ],
      },
    };
  },
  methods: {
    edittask() {
      var url = "http://pi.deadpoetspoon.xyz:7900/tasks/" + this.task.id + "/";
      this.$axios
        .put(url, this.task)
        .then((response) => {
          this.$message({
            showClose: true,
            message: response,
            type: "success",
          });
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
    deletetask() {
      var url = "http://pi.deadpoetspoon.xyz:7900/tasks/" + this.task.id;
      this.$axios
        .delete(url)
        .then((response) => {
          this.$message({
            showClose: true,
            message: response,
            type: "success",
          });
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
    createtask(){
      var url = "http://pi.deadpoetspoon.xyz:7900/tasks/";
      this.$axios
        .post(url, this.task)
        .then((response) => {
          this.$message({
            showClose: true,
            message: response,
            type: "success",
          });
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
    }
  },
};
</script>