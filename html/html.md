## DOCTYPE 
1. 用于告知浏览器应该以什么样的文档类型去解析文档，不同的渲染模式会影响浏览器对CSS 、Javascript 脚本的解析，所以必须放在第一行
2. 浏览器渲染页面两种方式
   1. CSS1Compat:标准模式，以高标准呈现
   2. BackCompat:怪异模式，比较宽松小猴兼容的方式显示

## src 和 href 区别
1. 相同:都是引入外部资源的
2. 不同:
    1. src 解析的时候会暂停其他资源的处理，所以要放到最后面
    2. href 不会暂停其他资源的引用
   
## script 标签中的defer和async区别
1. 相同点: 都是异步加载外部的脚本文件，且不会阻塞页面的解析
2. 不同点: 
    1. 执行顺序：async 不能保证加载顺序; defer 保证加载顺序
    2. 脚本是否并行执行:async属性，表示后续文档的加载和执行与js脚本的加载和执行是并行进行的，即异步执行

## 常见的meta标签有哪些
1. charset: 描述html文档编码类型
2. keywords: 页面关键词
3. description: 页面描述
4. refresh: 页面重定向和刷新
5. viewport: 适配移动端

## HTML5新标签
1. 新增语义化标签：nav、header、footer、aside、section、article
2. 音频、视频标签：audio、video
3. 数据存储：localStorage、sessionStorage
4. canvas（画布）、Geolocation（地理定位）、websocket（通信协议）
5. input标签新增属性：placeholder、autocomplete、autofocus、required
6. history API：go、forward、back、pushstate


## Data URL
1. 就是将图片资源转为Base64 直接嵌入网页
2. 优点是减少http请求
3. 缺点是:Base64编码后图片图片会比转换之前的图片大上三分之一，并且不可以缓存