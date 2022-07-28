1. IOS 输入框大小需要 16px 要不然让输入的时候，会放大页面，或者页面在html添加 mate 字段，使其禁止缩放
2. Ios 点击按钮，弹出输入框并且需要拉起软键盘的时候，可以吧 按钮换成 label 标签，label 的for 属性就是 input 的 id
3. ios 输入的时候，会把页面出现把页面网上顶，并且无法复原的情况，解决办法 

    ~~~ javascript
   $("input,textarea").on("blur", function () {
            window.scroll(0, 0);
        });
    }
    ~~~