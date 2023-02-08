<template>
  <div class="option-change-container">
    <a-row v-if="type === 'option' || type === 'tab'" :gutter="8">
      <div class="option-change-box" v-for="(val, index) in value" :key="index">
        <a-col :span="9"><Input v-model="val.label" placeholder="名称"/></a-col>
        <a-col :span="9"><Input v-model="val.value" placeholder="值"/></a-col>
        <a-col :span="6"
          ><div @click="handleDelete(index)" class="option-delete-box">
            <a-icon type="delete" /></div
        ></a-col>
      </div>
      <a-col :span="24"><a @click="handleAdd">添加</a></a-col>
    </a-row>

    <a-row v-if="type === 'rules'" :gutter="8">
      <a-form-item label="最大值" class="no-border">
        <InputNumber v-model="max" placeholder="最大值" />
        <Input placeholder="提示信息" />
      </a-form-item>
      <a-form-item label="最小值" class="no-border">
        <InputNumber placeholder="最小值" />
        <Input placeholder="提示信息" />
      </a-form-item>
      <span v-for="(val, index) in value" :key="index">
        <div class="option-change-box" v-if="index !== 0">
          <a-col :span="18"
            ><Input v-model="val.message" placeholder="提示信息"
          /></a-col>
          <a-col :span="18"
            ><Input v-model="val.pattern" placeholder="正则表达式pattern"
          /></a-col>
          <a-col :span="6"
            ><div @click="handleDelete(index)" class="option-delete-box">
              <a-icon type="delete" /></div
          ></a-col>
        </div>
      </span>
      <a-col :span="24"><a @click="handleAddRules">增加校验</a></a-col>
    </a-row>
    <a-row v-else-if="type === 'colspan'" :gutter="8">
      <div class="option-change-box" v-for="(val, index) in value" :key="index">
        <a-col :span="18"
          ><InputNumber
            style="width:100%"
            :max="24"
            v-model="val.span"
            placeholder="名称"
        /></a-col>
        <a-col :span="6"
          ><div @click="handleDelete(index)" class="option-delete-box">
            <a-icon type="delete" /></div
        ></a-col>
      </div>
      <a-col :span="24"><a @click="handleAddCol">添加</a></a-col>
    </a-row>
  </div>
</template>
<script>
/*
 * author kcz
 * date 2019-11-20
 * description 修改多选、下拉、单选等控件options的组件，添加移除校验规制的组件
 */
import { pluginManager } from "../../utils/index";
const Input = pluginManager.getComponent("input").component;
const InputNumber = pluginManager.getComponent("aNumber").component;
export default {
  name: "KChangeOption",
  components: {
    Input,
    InputNumber,
  },
  props: {
    value: {
      type: Array,
      required: true,
    },
    type: {
      type: String,
      default: "option",
    },
  },
  data() {
    return {
      max: null,
      maxMsg: "",
      min: null,
      minMsg: "",
    };
  },
  // watch: {
  //   max: {
  //     // value 需要深度监听及默认先执行handler函数
  //     handler(val) {
  //       console.log(val);
  //       const index = this.value.findIndex((item) => item?.validator);
  //       if (index !== -1) {
  //         this.value[index].validator = (rule, value, callback) => {
  //           if (val && value < val) {
  //             callback(`最大值不能超过${val}`);
  //           }
  //           callback();
  //         };
  //       } else {
  //         this.value = [
  //           ...this.value,
  //           {
  //             validator: (rule, value, callback) => {
  //               if (val && value < val) {
  //                 callback(`最大值不能超过${val}`);
  //               }
  //               callback();
  //             },
  //           },
  //         ];
  //       }
  //       console.log(this.value,JSON.stringify(this.value));
  //     },
  //     immediate: true,
  //     deep: true,
  //   },
  // },
  methods: {
    handleAdd() {
      // 添加
      const addData = [
        ...this.value,
        {
          value: `${this.value.length + 1}`,
          label: "选项" + (this.value.length + 1),
          list: this.type === "tab" ? [] : undefined,
        },
      ];
      this.$emit("input", addData);
    },
    handleAddCol() {
      // 添加栅格Col
      const addData = [
        ...this.value,
        {
          span: 12,
          list: [],
        },
      ];
      this.$emit("input", addData);
    },
    handleAddRules() {
      const addData = [
        ...this.value,
        {
          pattern: "",
          message: "",
        },
      ];
      this.$emit("input", addData);
    },
    handleDelete(deleteIndex) {
      // 删除
      this.$emit(
        "input",
        this.value.filter((val, index) => index !== deleteIndex)
      );
    },
  },
};
</script>

<style lang="less" scoped>
.no-border {
  border-bottom: unset !important;
}
</style>
