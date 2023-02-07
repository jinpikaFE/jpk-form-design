<template>
  <div class="container">
    <a-tabs default-active-key="1" :animated="false">
      <a-tab-pane key="1">
        <span slot="tab">
          <a-icon type="desktop" />
        </span>
        <Build />
      </a-tab-pane>
      <a-tab-pane key="2">
        <span slot="tab">
          <a-icon type="tablet" />
        </span>
        <div class="box">
          <iframe class="phoneBox" :src="iframeSrc"></iframe>
        </div>
      </a-tab-pane>
    </a-tabs>
  </div>
</template>
<script>
import Build from "../build";
export default {
  name: "Demo",
  data() {
    return {
      iframeSrc: "",
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
  components: { Build },
  mounted() {
    this.iframeSrc = `${window.location.origin}/#/build`;
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

<style lang="less" scoped>
.container {
  ::v-deep .ant-tabs-nav-scroll {
    display: flex;
    justify-content: center;
  }
}

.box {
  display: flex;
  justify-content: center;

  .phoneBox {
    width: 375px;
    height: 90vh;
    border: 1px solid #e8e8e8;
    overflow: auto;
    padding: 10px;
    border-radius: 16px;
  }
}
</style>
