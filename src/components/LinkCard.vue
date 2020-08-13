<template>
  <el-card shadow="hover">
    <el-link :icon="iconname" :href="linkurl">{{linktext}}</el-link>
  </el-card>
</template>
<script>
export default{
  name:'LinkCard',
  props:['iconname','linkurl','linktext'],
  data(){
    return{
      
    };
  }
}
</script>
<style>
</style>
