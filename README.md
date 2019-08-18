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
## my-toast
### 结构
+ toast组件自身，dom结构以及data，并在其生命周期完成在页面中的挂载与销毁
+ 组件外构建的一层代理，用于控制多个toast在页面中的显示顺序
### 方法
prototype添加方法
```js
let instances = []
let initIndex = 0
Vue.prototype.$toast = (options = {} => {
  // 创建一个toast组件实例
  let instance = generateInstance(options)
  // 将单个toast存入队列
  instances.push(instance)
})
```
generateInstance()方法
```js
// 构造单个toast
const ToastConstructor = Vue.extend(Toast)
const verticalOffset = 16
function generateInstance(options) {
  // 创建一个Toast实例
  let instance = new ToastConstructor({
    propsData: options
  }).$mount(document.createElement('div'))
  if (typeof options.onclose === 'function')
  instance.onClose = options.onClose
  // 计算instance verticalOffset
  let id = 'toast_' + initIndex++
  instance.id = id
  // 初始化toast在空间中的垂直偏移量
  instance.verticalOffset = initVerticalOffset(instance.position)
  // 监听组件close
  instance.$once('toastClose', function() {
    const curInstance = this
    // 当Toast组件关闭时，重新计算垂直方向的偏移量
    updateVerticalOffset(curInstance)
    typeof curInstance.onClose === 'function' && curInstance.onClose()
  })
  return instance;
}
```