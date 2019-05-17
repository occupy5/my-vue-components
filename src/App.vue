<template>
  <div id="app">
    <!-- 实现方式1 -->
    <div class="list">
      <label>类型</label>
      <div class="list-item">
        <my-radio v-model="val1" :options="['喵星人', '汪星人']"></my-radio>
      </div>
      <label>性别</label>
      <div class="list-item">
        <my-radio v-model="val2" :options="['小公主', '小王子']"></my-radio>
      </div>
    </div>

    <!-- 实现方式2 -->
    <div class="list">
      <div class="list-item">
        <label>类型</label>
        <my-radio-group v-model="val3">
          <my-radio-button value="1" :checked="ischecked">喵星人</my-radio-button>
          <my-radio-button value="2">汪星人</my-radio-button>
        </my-radio-group>
      </div>
      <div class="list-item">
        <label>性别</label>
        <my-radio-group v-model="val4">
          <my-radio-button value="3">小公主</my-radio-button>
          <my-radio-button value="4">小王子</my-radio-button>
        </my-radio-group>
      </div>
    </div>
  </div>
</template>

<script>
  import MyRadio from './components/MyRadio'
  import MyRadioButton from './components/MyRadioButton'
  import MyRadioGroup from './components/MyRadioGroup'
  export default {
    name: 'app',
    data() {
      return {
        val1: '',
        val2: '',
        val3: '',
        val4: '',
        isdisabled: true,
        ischecked: true
      }
    },
    components: {
      MyRadio,
      MyRadioButton,
      MyRadioGroup
    }
  }
</script>

<style>
  #app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    color: #2c3e50;
    margin-top: 60px;
  }
</style>