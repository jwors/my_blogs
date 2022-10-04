## css选择器
1.!important > 行内样式 >  id(#app) > 类 (class) | 属性选择器 (a[ref='eee']) | 伪类选择器(li:active) > 标签选择器 || 伪元素选择器(li::before) > 通配符选择器

## css组合器
1. + fgh  ——相邻兄弟选择器 (+) 介于两个选择器之间，当第二个元素紧跟在第一个元素之后，并且两个元素都是属于同一个父元素的子元素，则第二个元素将被选中
2. ~ 选择兄弟元素——兄弟选择符，位置无须紧邻，只须同层级，A~B 选择A元素之后所有同层级B元素

## css 等比
1. aspect-ratio

## 伪类和伪元素区别
1. 伪类前面一个:，伪元素 ::
2. 常用的伪元素: ::before  ::after  ::selection

## display 属性
1. none、block、inline、inline-block、list-item、table、inherit

## transition和animation的区别
1. transition是过度属性，强调过度，它的实现需要触发一个事件（比如鼠标移动上去，焦点，点击等）才执行动画
2. animation是动画属性，它的实现不需要触发事件，设定好时间之后可以自己执行，且可以循环一个动画

## 伪元素和伪类的区别和作用
1. 伪元素:在内容元素的前后插入额外的元素或样式，但是这些元素实际上并不在文档中生成。它们只在外部显示可见，但不会在文档的源代码中找到它们，因此，称为“伪”元素。
2. 伪类：将特殊的效果添加到特定选择器上。它是已有元素上添加类别的，不会产生新的元素

## 盒模型
1. 标准盒模型
    > 标准盒模型的width和height属性的范围只包含了content,content-box
2. IE盒模型(怪异盒模型)    
    > IE盒模型的width和height属性的范围包含了border、padding和content,border-box

## css单位
1. px、%、em(相对父元素)、rem(相对跟元素)
   
## BFC
1. 就是格式化上下文，通俗点来说就是一个容器，在这个容器中按照一定规则进行物品摆放，并且不会影响其它环境中的物品
2. 触发:
    1. 设置浮动除了none除外的值
    2. display 值为：inline-block、table-cell、table-caption、fle
    3. overflow 值为：hidden、auto、scroll

3. 解决了什么
    1. 在BFC中上下相邻的两个容器的margin会重叠
    2. 解决高度塌陷的问题

## position
1. absolute、relative、fixed、static、inherit

## 1像素问题
1. 1px 问题指的是：在一些 Retina屏幕 的机型上，移动端页面的 1px 会变得很粗，呈现出不止 1px 的效果。原因很简单——CSS 中的 1px 并不能和移动设备上的 1px 划等号。
2. 解决:
    1. 思路是先放大、后缩小：在目标元素的后面追加一个 ::after 伪元素，让这个元素布局为 absolute 之后、整个伸展开铺在目标元素上，然后把它的宽和高都设置为目标元素的两倍，border值设为 1px。接着借助 CSS 动画特效中的放缩能力，把整个伪元素缩小为原来的 50%。此时，伪元素的宽高刚好可以和原有的目标元素对齐，而 border 也缩小为了 1px 的二分之一，间接地实现了 0.5px 的效果。
    ~~~css
    #container[data-device="2"] {
    position: relative;
    }
    #container[data-device="2"]::after{
        position:absolute;
        top: 0;
        left: 0;
        width: 200%;
        height: 200%;
        content:"";
        transform: scale(0.5);
        transform-origin: left top;
        box-sizing: border-box;
        border: 1px solid #333;
        }
    }
    ~~~



