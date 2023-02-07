<template>
  <div>
    <k-form-build :value="jsonData" ref="KFB" @submit="handleSubmit" />

    <!-- <button @click="getData">提交</button>
    <button @click="setData">数据回显</button> -->
  </div>
</template>
<script>
export default {
  name: "Demo",
  data() {
    return {
      jsonData: {
        list: [],
        config: {
          layout: "horizontal",
          labelCol: { xs: 4, sm: 4, md: 4, lg: 4, xl: 4, xxl: 4 },
          labelWidth: 100,
          labelLayout: "Grid",
          wrapperCol: { xs: 24, sm: 24, md: 15, lg: 15, xl: 15, xxl: 15 },
          hideRequiredMark: false,
          customStyle: "",
        },
      },
    };
  },
  methods: {
    handleSubmit(p) {
      // 通过表单提交按钮触发，获取promise对象
      p()
        .then((res) => {
          // 获取数据成功
          alert(JSON.stringify(res));
        })
        .catch((err) => {
          console.log(err, "校验失败");
        });
    },
    show() {
      this.$refs.KFB.show(["date_1619948975172"]);
    },
    hide() {
      this.$refs.KFB.hide(["date_1619948975172"]);
    },
    disable() {
      this.$refs.KFB.disable(["date_1619948975172"]);
    },
    enable() {
      this.$refs.KFB.enable(["date_1619948975172"]);
    },
    getData() {
      // 通过函数获取数据
      this.$refs.KFB.getData()
        .then((res) => {
          // 获取数据成功
          alert(JSON.stringify(res));
        })
        .catch((err) => {
          console.log(err, "校验失败");
        });
    },
    setData() {
      this.$refs.KFB.setData({
        date_1619948975172: "2019-12-12",
      });
    },
  },
  mounted() {
    /** 获取本地缓存 */
    if (window.localStorage.getItem("currentRecord")) {
      this.jsonData.list = JSON.parse(
        window.localStorage.getItem("currentRecord")
      )?.list;
      this.jsonData.config = JSON.parse(
        window.localStorage.getItem("currentRecord")
      )?.config;
    }
  },
};
</script>
