<template>
  <div id="app">
    <!-- my-radio组件 -->
    <!-- 实现方式1 -->
    <div class="list">
      <h2>my-radio组件</h2>
      <label>类型test</label>
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
    <!-- my-input组件 -->
    <h2>my-input组件</h2>
    <my-input placeholder="请输入内容">
      <div slot="prepend">
        <!-- <span>前缀</span> -->
      </div>
      <div slot="append">
        <span>后缀</span>
      </div>
    </my-input>
    <div class="svg-test">
      <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24">
        <g>
          <path fill="none" d="M0 0h24v24H0z"></path>
          <path
            fill-rule="nonzero"
            d="M6.94 5a2 2 0 1 1-4-.002 2 2 0 0 1 4 .002zM7 8.48H3V21h4V8.48zm6.32 0H9.34V21h3.94v-6.57c0-3.66 4.77-4 4.77 0V21H22v-7.93c0-6.17-7.06-5.94-8.72-2.91l.04-1.68z"
          ></path>
        </g>
      </svg>
    </div>
    <!-- 分页组件 -->
    <h2>my-pagination组件</h2>
    <my-pagination
            class="pagination-danger"
            v-model="infoPagination"
            with-text
            :page-count="0"
    >
    </my-pagination>
  </div>
</template>

<script>
import MyRadio from "./components/MyRadio";
import MyRadioButton from "./components/MyRadioButton";
import MyRadioGroup from "./components/MyRadioGroup";
import MyInput from "./components/MyInput";
import MyPagination from "./components/MyPagination";
export default {
  name: "app",
  data() {
    return {
      val1: "",
      val2: "",
      val3: "",
      val4: "",
      isdisabled: true,
      ischecked: true,
      defaultPagination: 3,
      infoPagination: 3
    };
  },
  components: {
    MyRadio,
    MyRadioButton,
    MyRadioGroup,
    MyInput,
    MyPagination
  }
};
</script>

<style>
/* @import url("https://fonts.googleapis.com/css?family=Anton|Kumar+One+Outline&display=swap"); */
#app {
  /* font-family: "Kumar One Outline", cursive; */
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  margin-top: 60px;
}
.svg-test {
  height: 20px;
  width: 20px;
}
</style>