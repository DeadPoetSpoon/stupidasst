<template>
  <div id="app">
    <el-container>
      <el-aside width="155px">
        <NavMenu @select="update"/>
      </el-aside>
      <el-container>
        <el-main>
          <keep-alive>
            <component v-bind:is="current" msg="sssss"></component>
          </keep-alive>
          <el-dialog
              :visible.sync="dialogAdmin">
            <el-card shadow="hover"><el-link icon="el-s-custom" href="http://pi.deadpoetspoon.xyz:7900/admin/">Django管理面板</el-link></el-card>
            <span slot="footer" class="dialog-footer">
              <el-button @click="dialogAdmin = false">取 消</el-button>
            </span>
          </el-dialog>
        </el-main>
      </el-container>
    </el-container>
  </div>
</template>

<script>
import NavMenu from './components/NavMenu.vue'
import HelloWorld from './components/HelloWorld.vue'
import LinkPanel from './components/LinkPanel.vue'
import TaskList from './components/TaskList.vue'
export default {
  name: 'app',
  data(){
    return {
      current:'LinkPanel',
      dialogAdmin:false
    };
  },
  methods:{
    update(com){
      console.log(com);
      if(com == "Admin"){
        this.dialogAdmin = true;
        return;
      }
      this.current = com;
    }
  },
  components: {
    NavMenu,
    HelloWorld,
    LinkPanel,
    TaskList
  }
} 
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}
</style>
