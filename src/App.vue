<template>
  <div id="app">
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
  </div>
</template>

<script>
  import MyRadio from './components/MyRadio'

  export default {
    name: 'app',
    data() {
      return {
        val1: '',
        val2: '',
        isdisabled: true,
        ischecked: true
      }
    },
    components: {
      MyRadio
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