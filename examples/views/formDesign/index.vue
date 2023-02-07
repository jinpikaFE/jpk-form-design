<template>
  <div>
    <k-form-design
      hideResetHint
      @handlePagePreview="handlePagePreview"
      showToolbarsText
    />
  </div>
</template>

<script>
export default {
  name: "formDesign",
  methods: {
    handlePagePreview() {
      this.$router.push({
        //核心语句
        path: "/demo", //跳转的路径
        query: {
          //路由传参时push和query搭配使用 ，作用时传递参数
          id: this.id,
        },
      });
    },
  },
};
</script>
