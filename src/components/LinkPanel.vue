<template>
  <el-col>
    <el-row :gutter="24" v-loading="loading">
      <el-col :span="6">
        <el-row :gutter="12">
          <el-tag>工具</el-tag>
        </el-row>
        <br />
        <el-divider></el-divider>
        <el-row :gutter="12" v-for="tool in tools" :key="tool.id">
          <LinkCard v-bind="tool" />
          <br />
        </el-row>
      </el-col>
      <el-col :span="6">
        <el-row :gutter="12">
          <el-tag>应用</el-tag>
        </el-row>
        <br />
        <el-divider></el-divider>
        <el-row :gutter="12" v-for="app in apps" :key="app.id">
          <LinkCard v-bind="app" />
          <br />
        </el-row>
      </el-col>
      <el-col :span="6">
        <el-row :gutter="12">
          <el-tag>娱乐</el-tag>
        </el-row>
        <br />
        <el-divider></el-divider>
        <el-row :gutter="12" v-for="amusement in amusements" :key="amusement.id">
          <LinkCard v-bind="amusement" />
          <br />
        </el-row>
      </el-col>
      <el-col :span="6">
        <el-row :gutter="12">
          <el-tag>其他</el-tag>
        </el-row>
        <br />
        <el-divider></el-divider>
        <el-row :gutter="12" v-for="other in others" :key="other.id">
          <LinkCard v-bind="other" />
          <br />
        </el-row>
      </el-col>
    </el-row>
    <!--
<el-row :gutter="4">
  <el-button-group>
    <el-button type="primary" icon="el-icon-plus" :loading="loading" @click="dialogInsert = true">添加</el-button>
    <el-button type="primary" icon="el-icon-refresh" :loading="loading" @click="dialogUpdate = true">更新</el-button>
  </el-button-group>
  <el-dialog title="收货地址" :visible.sync="dialogInsert">
  <el-form :model="form">
    <el-form-item label="" label-width="120px">
      <el-input v-model="form.name" auto-complete="off"></el-input>
    </el-form-item>
    <el-form-item label="活动区域" label-width="120px">
    </el-form-item>
  </el-form>
  <div slot="footer" class="dialog-footer">
    <el-button @click="dialogFormVisible = false">取 消</el-button>
    <el-button type="primary" @click="dialogFormVisible = false">确 定</el-button>
  </div>
  </el-dialog>
</el-row>
    -->
  </el-col>
</template>

<script>
import LinkCard from "./LinkCard.vue";
export default {
  name: "LinkPanel",
  components: {
    LinkCard,
  },
  data() {
    return {
      tools: [],
      apps: [],
      amusements: [],
      others: [],
      loading: true,
    };
  },
  methods: {},
  mounted: function () {
    this.$axios
      .get("http://pi.deadpoetspoon.xyz:7900/links/?format=json")
      .then((response) => {
        var data = this;
        //console.log(response.data);
        response.data.forEach((link) => {
          switch (link.linktag) {
            case "Tool":
              data.tools.push(link);
              break;
            case "App":
              data.apps.push(link);
              break;
            case "Amusement":
              data.amusements.push(link);
              break;
            case "Other":
              data.others.push(link);
              break;
          }
        });
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
