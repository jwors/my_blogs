# 操作上的优化

## 防抖节流

1. 防抖 行为结束之后的操作

    ~~~javascript
    function debounce(func, wait) {
        let timeout;
        return function() {
            const context = this;
            const args = arguments;
            clearTimeout(timeout);
            timeout = setTimeout(function() {
            func.apply(context, args);
            }, wait);
        };
    }
    ~~~

2. 节流是每隔一段时间操作

    ~~~javascript
        function throttle (fn,waitTime = 1000) {
            let time = 0
            if (time) {
                return
            }
            time = setTimeout(() => {
                fn.apply(arguments)
            }, waitTime);
        }

    ~~~

## 区别

1. 防抖是操作结束之后触发，节流是每隔一段时间触发
2. 防抖是操作结束之后触发，节流是操作开始之后触发

## 理解代码

