# my-radio
仿照element写一个可拓展的vue radio，[源码地址](https://github.com/ElemeFE/element/blob/dev/packages/radio/src/radio.vue)
## model API
这里主要使用了model这个api
```js
Vue.component('my-checkbox', {
  model: {
    prop: 'checked',
    event: 'change'
  },
  props: {
    // this allows using the `value` prop for a different purpose
    value: String,
    // use `checked` as the prop which take the place of `value`
    checked: {
      type: Number,
      default: 0
    }
  },
  // ...
})
```
具体[文档地址](https://cn.vuejs.org/v2/api/#model)
## radio组
重点：radio和radio-group之间的联动及数据绑定关系