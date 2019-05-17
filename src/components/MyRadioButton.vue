<template>
  <label
    class="radio"
    :class="[
        { 'checked': value === model },
        { 'is-disabled': isDisabled }
    ]"
    @click.stop="handleClick"
  >
    <span class="radio-inner"></span>
    <input
      class="radio-hide"
      type="radio"
      :disabled="isDisabled"
      v-bind="$attrs"
      :value="model"
      @click.stop
    >
    <slot></slot>
  </label>
</template>

<script>
export default {
  name: 'MyRadioButton',
  props: {
    value: {
      type: [String, Number],
      required: true
    },
    disabled: {
      type: [Boolean],
      default: false
    },
    checked: {
      type: [Boolean],
      default: false
    },
    propValue: {
      type: [String, Number]
    }
  },
  model: {
    prop: "propValue",
    event: "select"
  },
  computed: {
    // 通过$parent取得父组件，然后判断其组件名称，确定当前组件是否被group组件包裹
    isGroup() {
      return this.$parent.$options._componentTag === "my-radio-group";
    },
    isDisabled() {
      return this.$parent.disabled || this.disabled;
    },
    model: {
      get() {
        return this.isGroup ? this.$parent.value : this.propValue;
      },
      set(newValue) {
        this.isGroup
          ? this.$parent.$emit("select", newValue)
          : this.$emit("select", newValue);
      }
    }
  },
  methods: {
    handleClick() {
      !this.isDisabled && (this.model = this.value);
    }
  }
};
</script>
<style lang="scss" scoped>
.radio {
  display: inline-flex;
  align-items: center;
  vertical-align: middle;
  user-select: none;
  $radio-size: 14px;
  $radio-space: 8px;
  .radio-inner {
    margin-right: $radio-space;
    display: inline-block;
    width: $radio-size;
    height: $radio-size;
    border: 1px solid #ccc;
    border-radius: 50%;
  }
  $radio-checked-size: 16px;
  &.checked {
    .radio-inner {
      width: $radio-checked-size;
      height: $radio-checked-size;
      box-sizing: border-box;
      border: 5px solid #5c5cee;
    }
  }
  &.is-disabled {
    user-select: none;
    cursor: not-allowed;
    opacity: 0.5;
    &:hover {
      opacity: 0.5;
    }
  }
  .radio-hide {
    display: none;
  }
}
</style>
