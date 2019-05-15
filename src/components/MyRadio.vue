<template>
  <div>
    <label v-for="(option, index) in options" :key='index'>
      <input class="my-radio" type="radio" ref="radio" :value="option" v-model="localValue" :disabled="disabled">{{option}}
    </label>
  </div>
</template>
<script>
  export default {
    name: 'MyRadio',
    // model: {
    //   prop: 'model',
    //   event: 'change'
    // },
    props: {
      options: {
        type: Array,
        required: true
      },
      value: {
        type: [String, Number],
        required: true
      },
      checked: {
        type: Boolean,
        default: false
      },
      disabled: {
        type: Boolean,
        default: false
      }
    },
    computed: {
      localValue: {
        get() {
          return this.value
        },
        set(value) {
          this.$emit('input', value)
        }
      }
    }
  }
</script>
<style>
  .my-radio {
    width: 14px;
    height: 14px;
    border-radius: 50%;
    border: 1px solid #4693fe;
    display: inline-block;
    position: relative;
  }

  .my-radio.disabled {
    border-color: #ccc;
  }

  .my-radio::after {
    content: '';
    width: 10px;
    height: 10px;
    border-radius: 50%;
    display: inline-block;
    position: absolute;
    left: 50%;
    top: 50%;
    margin: -5px 0 0 -5px;
    background-color: #4693fe;
    transition: all .5s ease;
    opacity: 0;
    transform: scale(0);
  }

  .my-radio.disabled::after {
    background-color: #ccc;
  }

  .my-radio.checked::after {
    opacity: 1;
    transform: scale(1);
  }

  .my-radio input[type=radio] {
    opacity: 0;
    margin: 0;
  }
</style>