# Vue源码 2.6.14

## watch中的deep做了什么？ src/core/observer/watcher.js
> 在get中的 <b>finally</b> 判断是否使用 <b>deep</b>
~~~ javascript

const seenObjects = new Set()

export function traverse (val: any) {
  _traverse(val, seenObjects)
  seenObjects.clear()
}

function _traverse (val: any, seen: SimpleSet) {
  let i, keys
  const isA = Array.isArray(val)
  // 不是数组 或者是对象(null) 就直接返回  这里也是一处优化点，判断当前 这个值是否是 当前这个页面的this 上 或者是被冻结的
  // 如果满足其一  就直接返回 不浪费性能
  if ((!isA && !isObject(val)) || Object.isFrozen(val) || val instanceof VNode) {
    return
  }
  // 不满足上面的条件之后 才会进行深度的监听 
  if (val.__ob__) {
    const depId = val.__ob__.dep.id
    if (seen.has(depId)) {
      return
    }
    seen.add(depId)
  }
  if (isA) {
    i = val.length
    while (i--) _traverse(val[i], seen)
  } else {
    keys = Object.keys(val)
    i = keys.length
    while (i--) _traverse(val[keys[i]], seen)
  }
}
~~~

## Vue响应式原理
通过 /state/core/instance 中的 initState 方法,对script内的属性进行操作
~~~ javascript
  export function initState (vm: Component) {
    vm._watchers = []
    const opts = vm.$options
    if (opts.props) initProps(vm, opts.props)
    if (opts.methods) initMethods(vm, opts.methods)
    if (opts.data) {
      initData(vm)
    } else {
      observe(vm._data = {}, true /* asRootData */)
    }
    // 进入 计算属性
    if (opts.computed) initComputed(vm, opts.computed)
    if (opts.watch && opts.watch !== nativeWatch) {
      // 构建 watch
      initWatch(vm, opts.watch)
    }
  }
~~~