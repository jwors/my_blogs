## 事件

#### 事件冒泡

 > [事件](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Building_blocks/Events#%E4%BA%8B%E4%BB%B6%E5%A7%94%E6%89%98)冒泡的顺序是从内到外的,它伴随的问题就是当**div**和**button**都有事件的时候，哪怕只想触发button的，但是有了冒泡依旧会触发div上的。

```html

 <div>
  <button>click</button>
 </div>
  
```

#### 事件捕获
 > [事件捕获](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Building_blocks/Events#%E4%BA%8B%E4%BB%B6%E5%A7%94%E6%89%98)