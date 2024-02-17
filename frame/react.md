# React 面试题

### 虚拟dom

#### 优点

 > 首先虚拟dom本质是以js中的对象来解释**dom**元素，从而对对象操作不会引起页面的绘制  

 1. 性能优化
       1. **直接减少操作dom的次数:** 框架会在内存中创建虚拟dom，然后通过新旧对比后，  只有真正变化的内容才会被操作到真实的dom上,并且不是每次改动都会，是批次化处理的，从而减少了直接操作dom的次数,并且减少了重绘和重拍，
       2. **异步更新:** 虚拟DOM的实现通常会采用异步更新的机制，即将状态变化的处理推迟到下一个事件循环中执行。这样，即便有多次状态变化，也可以将它们合并到一次更新中，减少了直接操作DOM的次数
 2. 跨平台: 因为对真实dom的操作转为对虚拟dom的操作，从而减少了不同平台下的渲染差异
 3. 提高开发效率：开发者先对与之前，就不用过于关注dom操作，只需关注数据和状态处理
 4. 方便状态管理：虚拟DOM通常与响应式数据绑定结合使用，当数据改变，框架能够识从而更新虚拟dom后反映到真实dom

#### 缺点

  1. 内存消耗: 由于框架会在内存中维护一份虚拟dom树，当以当大型应用的时候会对性能产生影响
  2. 首次渲染: 由此首次渲染会将虚拟dom转为真实dom,这个过程会增加开销。
  3. 极致性能优化: 有时候，直接的DOM操作可能比虚拟DOM更为高效，尤其是对于一些特定的DOM操作，例如直接插入大量元素

***

### Filber设计思路

> 改设计方法的目的是为了解决React在大型应用的时出可能出现的性能问题，特别是在处理复杂的用户界面、大量组件和频繁更新时。**举个例子:**当更新一个组件为1ms，如果有200个组件那就是200ms，在更新的过程中浏览器的主线程就会专注更新操作，当在200ms内用户在输入框内输入内容的时候是不会获得响应的，只有等主线程处理完成之后才可以，这期间就会出现页面卡顿。而**Filber**就是为了解决卡顿问题

  1. 实现了基于优先级和[requestIdLeCallback](https://developer.mozilla.org/zh-CN/docs/Web/API/Window/requestIdleCallback) 的循环任务调度算法，将渲染虚拟dom、diff任务拆分为多个小任务，这样可以随时进行终止、恢复，同时跟根据每个任务的优先级来执行任务
  2. Filber 是 **render/update** 分片，拆成多个小任务来执行，每次检查render tree上的部分节点，做完之后，若当前一帧(16ms)内还有足够时间，就会做下一个小任务，不够就停止操作
  3. 不同的任务是分优先级
     1. Immediate:最高级
     2. UseBlocking: 用户交互的，需要及时反馈
     3. Normal: 网络请求等不需要用户立即感受的
     4. Low 低等级，可以延后但是要执行的
     5. Idle 最低等级 可以不执行

***

### React state 那些事

#### 更新机制 异步OR同步

   1. 在react18之前，在Promise的状态更新、js原生事件、setTimeout、setInterval..中是同步的。在react的合成事件中，是异步的。在[React18](https://github.com/reactwg/react-18/discussions/21)之后就是异步的
   2. 所谓的合成事件就是react里面的机制，原生事件就是 document,getElementById('#dd') 绑定的事件

```javascript
/* by https://github.com/reactwg/react-18/discussions/21 */

import { flushSync } from 'react-dom'; // Note: react-dom, not react

function handleClick() {
  flushSync(() => {
    setCounter(c => c + 1);
  });
  // React has updated the DOM by now
  flushSync(() => {
    setFlag(f => !f);
  });
  // React has updated the DOM by now
}
```

***

### 合成事件

  > 什么是合成事件：是指将原生[事件](https://developer.mozilla.org/zh-CN/docs/Learn/JavaScript/Building_blocks/Events)合成为一个React事件，目的是解决浏览器的不一致性。
  从v17.0.0开始, React 不会再将事件处理添加到 document 上, 而是将事件处理添加到渲染 React 树的根 DOM 容器中,
