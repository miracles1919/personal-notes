1、写一个有效的算法完成矩阵搜索，这个矩阵有如下特点：

1)  矩阵中的每行数字都是经过排序的，从左到右依次变大。

2)  每行的第一个数字都比上一行的最后一个数字大

例如：
[
  [2,4,8,9],
  [10,13,15,21],
  [23,31,33,51]
]

实现一个函数，搜索这个数组
输入：4，返回：true
输入：3，返回：false

```javascript
// 方法1
function search(arr, value){
  for(let i = 0, len = arr.length; i < len; i++) {
  	for(let j = 0, inner = arr[i].length; j < inner; j++) {
      let innerArr = arr[i];
      if (value > innerArr[innerArr.length - 1]) break;
      if (innerArr[j] === value) return true;
  	}
  }
  return false
}

// 方法2
function search2(arr, value){
  let list = []
  arr.forEach(item => {
    list = [...list, ...item]
  })
  return list.indexOf(value) !== -1
}
```

2、有一个数组[7,8,3,5,1,2,4,3,1]，写一个方法来“去重”并“输出从大到小”的“货币格式”
期望结果："8,754,321"
```javascript
// 方法1
function format(arr){
  let list = [...new Set(arr)].sort().reverse()
  let str = list.join('')
  let result = ''
  while(str.length > 0){
    result = `,${str.slice(-3)}` + result
    str = str.slice(0, str.length - 3)
  }
  return result.splice(1)
}

// 方法2
function format2(arr){
  let list = [...new Set(arr)].sort().reverse()
  let str = list.join('')
  return parseInt(str).toLocaleString()
}
```

3、有一个数组：
const imgs = ['url1','url2','url3',...];

请实现效果：
按照图片数组顺序队列加载图片（注：加载完一张再加载下一张）
```javascript

// 方法1
function imgLoad (imgs) {
  if (imgs.length > 0) {
    let img = new Image()
    img.src = imgs[0]
    img.onload = function () {
      console.log('load', imgs[0])
      if (imgs.length > 1) {
        imgLoad(imgs.slice(1))
      }
    }
    img.onerror = function () {
      throw ('error happen')
    }
  }
}

// 方法2
async function imgLoad2 (imgs) {
  for (let img of imgs){
    await load(img)
  }
  function load(url) {
    return new Promise((resolve) => {
      let img = new Image()
      img.src = url
      img.onload = function () {
        console.log('load', url)
        resolve()
      }

      img.onerror = function () {
        throw ('error happen')
      }
    })
  }
}

```