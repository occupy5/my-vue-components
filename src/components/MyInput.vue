<template>
  <!-- 动态传入前后缀图标的样式 -->
  <div 
    :class="[
      'input',
      {
        'have-prefix-icon': prefixIcon,
        'have-suffix-icon': suffixIcon
      }
    ]"
  >
    <!-- 只有文本框的情况 -->
    <textarea
      v-if="type === 'textarea'"
      class="input_textarea-inner"
      :value="inputValue"
      v-bind="$attrs"
      v-on="inputListeners"
    />

    <!-- 添加前缀或者后缀 -->
    <template v-else>
      <!-- 前缀图标 -->
      <my-icon v-if="prefixIcon" class="input_icon" :name="prefixIcon" />
      <!-- 具名插槽实现自定义前缀 -->
      <slot name="prepend"></slot>
      <!-- 动态传入自定义前后缀的样式 -->
      <input 
        :class="[
          'input_input-inner',
          {
            'have-prepand': havePrepand,
            'have-append': haveAppend
          }
        ]"
        :type="type"
        :value="inputValue"
        v-bind="$attrs"
        v-on="inputListeners"
      />
      <!-- 自定义后缀 -->
      <slot name="append"></slot>
      <!-- 后缀图标 -->
      <my-icon v-if="suffixIcon" class="input_icon" :name="suffixIcon" />
    </template>
  </div>
</template>

<script>
export default {
  props: {
    type: {
      type: String,
      default: 'text'
    },
    value: {
      type: [String, Number],
      default: ''
    },
    prefixIcon: {
      type: String
    },
    suffixIcon: {
      type: String
    }
  },
  model: {
    prop: "value",
    event: "input"
  },
  data() {
    return {
      inputValue: ""
    }
  },
  // 访问自定义插槽内容
  computed: {
    havePrepand() {
      return this.$slots.prepend;
    },
    haveAppend() {
      return this.$slots.append;
    },
    inputListeners() {
      // 将所有对象合并为一个新对象
      return Object.assign({},
      // 从父级添加所有的监听器
      this.$listeners, 
      {
        //配合v-model
        input: event => this.$emit("input", event.target.value)
      })
    }
  },
  watch: {
    value: {
      handler(newVal) {
        this.inputValue = newVal
      }
    }
  }
}
</script>

<style lang="scss">
@import '../styles/global.scss';
.input {
  position: relative;
  display: flex;
  align-items: center;
  width: 100%;
  .input__icon {
    position: absolute;
    top: 0;
    bottom: 0;
    margin: auto auto;
    height: 1em;
    color: $disabled-color;
  }
  &.have-prefix-icon {
    .input__input-inner {
      padding-left: 24px;
    }
    .input__icon:first-child {
      left: 6px;
    }
  }
  &.have-suffix-icon {
    .input__input-inner {
      padding-right: 24px;
    }
    .input__icon:last-child {
      right: 6px;
    }
  }
  .input__input-inner,
  .input__textarea-inner {
    padding: 0 $m-offset;
    width: 100%;
    min-height: 32px;
    line-height: 32px;
    box-sizing: border-box;
    border: 1px solid $main-color;
    border-radius: $base-radius;
    color: $font-color;
    text-overflow: ellipsis;
    outline: none;
    transition: all 0.2s;
    &:focus {
      text-overflow: ellipsis;
      border: 1px solid $success-color;
      box-shadow: 0 0 5px 0 rgba($success-color, 0.5);
    }
    &:disabled {
      background-color: rgba($disabled-color, 0.25);
      color: $disabled-color;
      cursor: not-allowed;
    }
    &.have-prepand {
      border-radius: 0 $base-radius $base-radius 0;
      &.have-append {
        border-radius: 0 0 0 0;
      }
    }
    &.have-append {
      border-radius: $base-radius 0 0 $base-radius;
    }
  }
  .input__textarea-inner {
    min-height: 2.5em;
    line-height: 32px;
  }
}
</style>