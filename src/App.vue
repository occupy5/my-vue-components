<template>
  <div id="app">
    <div class="list">
      <label>类型</label>
      <div class="list-item">
        <my-radio v-model="val" value="1"></my-radio>
        <span>喵星人</span>
        <my-radio v-model="val" :checked="ischecked" value="2"></my-radio>
        <span>汪星人</span>
      </div>
      <label>性别</label>
      <div class="list-item">
        <my-radio v-model="val" value="3"></my-radio>
        <span>小王子</span>
        <my-radio v-model="val" :checked="ischecked" value="4"></my-radio>
        <span>小公主</span>
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
        val: '',
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