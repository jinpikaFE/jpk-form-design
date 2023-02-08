<template>
  <a-modal
    title="编辑数据"
    :visible="visible"
    @ok="handleImportJson"
    @cancel="handleCancel"
    cancelText="关闭"
    :destroyOnClose="true"
    wrapClassName="code-modal-9136076486841527"
    style="top:20px;"
    width="850px"
  >
    <div class="json-box-9136076486841527">
      <Codemirror
        style="height:100%;"
        ref="myEditor"
        v-model="jsonFormat"
      ></Codemirror>
    </div>
  </a-modal>
</template>
<script>
/*
 * author kcz
 * date 2019-11-20
 * description 导入json Modal
 */
import { pluginManager } from "../../../utils/index";
const Codemirror = pluginManager.getComponent("codemirror").component;
export default {
  name: "setDataModal",
  components: {
    Codemirror,
  },
  data() {
    return {
      visible: false,
      jsonFormat: ``,
      handleSetSelectItem: null,
    };
  },
  //   watch: {
  //     visible(val) {
  //       if (val) {
  //         this.jsonFormat = {};
  //       }
  //     },
  //   },
  computed: {
    editor() {
      // get current editor object
      return this.$refs.myEditor.editor;
    },
  },
  methods: {
    handleCancel() {
      this.visible = false;
    },
    handleImportJson() {
      console.log("test");
      this.$emit("onOk", this.jsonFormat);
    },
  },
};
</script>
