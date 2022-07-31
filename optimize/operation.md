# 操作上的优化
1. 防抖 行为结束之后的操作
    ~~~javascript
        function deBounce (fn,waitTime = 1000) {
            let time = 0
            if (time) {
                clearTimeout(time)
            }
            time = setTimeout(() => {
                fn.apply(arguments)
            }, waitTime);
        }
    ~~~
2. 节流是每隔一段时间操作 
    ~~~javascript
        function deBounce (fn,waitTime = 1000) {
            let time = 0
            if (time) {
                return
            }
            time = setTimeout(() => {
                fn.apply(arguments)
            }, waitTime);
        }
    ~~~