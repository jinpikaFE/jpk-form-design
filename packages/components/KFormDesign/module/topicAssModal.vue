<template>
  <a-modal
    title="题目关联"
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
      <a-form
        :form="form"
        layout="horizontal"
        :labelCol="{
          xs: 4,
          sm: 4,
          md: 4,
          lg: 4,
          xl: 4,
          xxl: 4,
        }"
        :wrapperCol="{
          xs: 24,
          sm: 24,
          md: 15,
          lg: 15,
          xl: 15,
          xxl: 15,
        }"
      >
        <a-form-item label="当前控件">
          {{ selectItem.label }} - {{ selectItem.key }}
        </a-form-item>
        <a-form-item
          v-for="(k, index) in form.getFieldValue('keys')"
          :key="k"
          :label="`关联问题 ${index}`"
          :required="true"
        >
          <Input
            v-decorator="[
              `names[${k}].test`,
              {
                validateTrigger: ['change', 'blur'],
                rules: [
                  {
                    required: true,
                    whitespace: true,
                    message: '请输入',
                  },
                ],
              },
            ]"
            style="width: 60%; margin-right: 8px"
          />
          <a-icon
            v-if="form.getFieldValue('keys').length > 1"
            class="dynamic-delete-button"
            type="minus-circle-o"
            :disabled="form.getFieldValue('keys').length === 1"
            @click="() => remove(k)"
          />
        </a-form-item>
        <a-form-item>
          <Button type="dashed" style="width: 60%" @click="add">
            <a-icon type="plus" /> Add field
          </Button>
        </a-form-item>
      </a-form>
    </div>
  </a-modal>
</template>
<script>
let id = 0;
import { pluginManager } from "../../../utils/index";
const Input = pluginManager.getComponent("input").component;
const Button = pluginManager.getComponent("aButton").component;

export default {
  name: "topicAssModal",
  components: {
    Button,
    Input,
  },
  data() {
    return {
      visible: false,
      handleSetSelectItem: null,
    };
  },
  props: {
    selectItem: {
      type: Object,
      required: true,
    },
  },
  computed: {
    editor() {
      // get current editor object
      return this.$refs.myEditor.editor;
    },
  },
  beforeCreate() {
    this.form = this.$form.createForm(this);
    this.form.getFieldDecorator("keys", { initialValue: [], preserve: true });
  },
  methods: {
    handleCancel() {
      this.visible = false;
    },
    handleImportJson() {
      this.form.validateFields((err, values) => {
        if (!err) {
          console.log("Received values of form: ", values);
          this.$emit("onOk", values);
        }
      });
    },
    remove(k) {
      const { form } = this;
      // can use data-binding to get
      const keys = form.getFieldValue("keys");
      // We need at least one passenger
      if (keys.length === 1) {
        return;
      }

      // can use data-binding to set
      form.setFieldsValue({
        keys: keys.filter((key) => key !== k),
      });
    },

    add() {
      const { form } = this;
      // can use data-binding to get
      const keys = form.getFieldValue("keys");
      const nextKeys = keys.concat(id++);
      // can use data-binding to set
      // important! notify form to detect changes
      form.setFieldsValue({
        keys: nextKeys,
      });
    },
  },
};
</script>
