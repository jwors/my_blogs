## 使用方法记录

1. 未使用 steup
   ~~~javascript
    export default {
        props:{
            num:number
        },
        emits:['sonGetValue'], // 不定义倒是可以用但是会warn
        // https://vuejs.org/api/composition-api-setup.html#basic-usage
        setup(props,context){ // props 不可以结构 context 可以结构
            const msg = ref(0)

            const transmit = ()=> {
                context.emit("sonGetValue", "asdasd");
            }

            return {
                count,
                transmit
            }
        }
    }
   ~~~

2. 使用 steup  
    ~~~javascript
        <script steup>
            //  这种使用更方便一些 
            const props = defineProps({
                text: Number,
                userInfo: {
                    type: Object,
                    require: true,
                },
            })

            const emit = defineEmits(['senFatherData'])

            const sendEmit = () => [
                emit("senFatherData", 1);
            ]
        </script>
    ~~~
