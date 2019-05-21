# vue 自定义组件
## my-radio
仿照element写一个可拓展的vue radio，[源码地址](https://github.com/ElemeFE/element/blob/dev/packages/radio/src/radio.vue)
### API
> model

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
### radio组
重点：radio和radio-group之间的联动及数据绑定关系

## my-input
### API
> $attrs
继承原生input上的相关属性，例如placeholder,maxlength.[v-bind="$attrs"](https://cn.vuejs.org/v2/api/#vm-attrs)

> $listeners
从父级元素上添加监听器，实现my-input组件上的change, focus, blur事件。[v-on="$listeners"](https://cn.vuejs.org/v2/guide/components-custom-events.html#%E5%B0%86%E5%8E%9F%E7%94%9F%E4%BA%8B%E4%BB%B6%E7%BB%91%E5%AE%9A%E5%88%B0%E7%BB%84%E4%BB%B6)
### 拓展
> 使用具名插槽实现自定义前后缀拓展

```js
<slot name="prepend"></slot>
<slot name="append"></slot>
```

