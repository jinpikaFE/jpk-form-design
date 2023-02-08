<template>
  <InputNumber v-bind="this.$attrs" v-model="numberValue"></InputNumber>
</template>
<script>
import { pluginManager } from "../../utils/index";
const InputNumber = pluginManager.getComponent("aNumber").component;
export default {
  name: "KNumber",
  props: ["record", "dynamicData", "value"],
  components: { InputNumber },
  computed: {
    numberValue: {
      get() {
        return this.value;
      },
      set(e) {
        this.$emit("change", e);
      },
    },
  },
};
</script>
