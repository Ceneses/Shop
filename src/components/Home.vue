<template>
  <div id="home">
    Home 组件
    <el-button type="info" @click="logout">退出</el-button>
  </div>
</template>

<script>
  export default {
    name: 'Home',
    methods: {
      logout () {
        window.sessionStorage.clear();
        this.$router.push('/login');
      }
    }
  };
</script>

<style scoped>

</style>
