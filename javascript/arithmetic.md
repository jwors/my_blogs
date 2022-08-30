# 算法

## 排序
~~~javascript
let arr = [2, 3, 4, 1, 3, 465, 74, 674, 875]
function sort(arr) {
    if(!Array.isArray(arr)){
        alert('请传入数组')
    }
    if(arr.length <= 1 ) {
        return
    }
    for(let i = 1; i < arr.length;i++) {
        for(let z = i; z > 0; z--){
            if(arr[z] < arr[z-1]){
                [arr[z],arr[z-1]] = [arr[z-1],arr[z]]
            }
        }
    }
}

function selectSort(arr) {
    if(!Array.isArray(arr)){
        alert('请传入数组')
    }
    if(arr.length <= 1 ) {
        return
    }
    
}
~~~