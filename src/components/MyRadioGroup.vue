<template>
  <div :class="['radio-group']" name="radio-group">
    <slot></slot>
  </div>
</template>
<script>
export default {
  name: "MyRadioGroup",
  props: {
    value: {},
    disabled: Boolean
  },
  model: {
    prop: "value",
    event: "select"
  },
  watch: {
    value(newValue) {
      this.$emit("change", newValue);
    }
  }
};
</script>
<style lang="scss" scoped>
.radio-group {
  display: flex;
  align-items: center;
  $base-space: 20px;
  .radio {
    &:not(:last-child) {
      margin-right: $base-space;
    }
  }
}
</style>
