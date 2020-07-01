<template>
  <el-menu
    :default-active="$route.path"
    class="el-menu-demo"
    mode="horizontal"
    @select="handleSelect"
  >
    <el-menu-item index="/">Пример пагинации</el-menu-item>
    <el-menu-item index="/about">Логика работы</el-menu-item>
    <el-menu-item class="github_navbar">
      <i class="el-icon-star-off"></i>
      <a href="https://github.com/stenready/pagination_instruction" target="_blank">GitHub</a>
    </el-menu-item>
    <el-menu-item class="email_navbar" style="color: forestgreen;"><i class="el-icon-s-promotion"></i>mastars2319@gmail.com</el-menu-item>
  </el-menu>
</template>

<script>
export default {
  data() {
    return {
      activeIndex: "/"
    };
  },
  methods: {
    handleSelect(key, path) {
      if (key) {
        if (this.$route.path !== key) this.$router.push(key);
      }
    }
  }
};
</script>

<style lang="scss">
.el-menu {
  display: flex;
  justify-content: flex-end;
}
.email_navbar{
  &:hover .el-icon-s-promotion{
    color:  forestgreen;
  }
}

</style>