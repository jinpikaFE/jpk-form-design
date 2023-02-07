<template>
  <div>
    <k-form-design hideResetHint @handlePagePreview="handlePagePreview" />
  </div>
</template>

<script>
export default {
  name: "formDesign",
  methods: {
    handlePagePreview() {
      this.$router.push({
        path: "/demo",
      });
    },
  },
};
</script>
