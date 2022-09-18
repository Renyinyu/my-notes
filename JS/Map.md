# Map

Map是一组键值对结构，用于解决以往对象不能使用对象作为键的问题

* 具有极快的查找速度
* 函数、对象、基本类型、都可以作为键或值

## 声明定义

可以接受一个数组作为参数

```javascript
  let map = new Map([
    ['tough.c', 'value tough'],
    ['tc', 'value tc']
  ])
  console.log(map.get('tough.c')) // value tough
```

使用实例方法<code>set</code>添加元素，支持链式操作

```javascript
let map = new Map()
map
  .set('tough.c', '硬帮帮')
  .set('英', 'english')

console.log(map.entries())
```

使用构造函数初始化创建的原理

```javascript
let map = new Map()
let arr = [
  ['tough.c', '硬帮帮'],
  ['eng', 'en-US']
]
arr.forEach([key, value] => {
  map.set(key, value)
})
```

对于键是对象的<code>Map</code>，键保存的是内存地址，值相同但内存地址不同的视为两个键

```javascript
let arr1 = ['tough.c']
let arr2 = ['tough.c']

let map = new Map()
map.set(arr1, 'tough.1')
map.set(arr2, 'tough.2')
console.log(map.get(arr1) == map.get(arr2)) // false
```

## 获取元素数量

```javascript
const map = new Map([
  ['touch', 'tc']
])

map.size // 1
```

## 元素检测

```javascript
const map = new Map([
  ['touch', 'tc']
])

map.has('touch') // true
```

## 读取元素

```javascript
const map = new Map([
  ['touch', 'tc']
])

map.get('touch') // tc
```

## 删除元素

使用<code>delete</code>方法删除单个元素

```javascript
const map = new Map([
  ['touch', 'tc']
])

map.delete('touch') 
console.log(map.get('touch')) // undefined
```

使用<code>clear</code>方法清除所有元素

```javascript
const map = new Map([
  ['touch1', 'tc1'],
  ['touch2', 'tc2'],
  ['touch3', 'tc3'],
])

map.clear() 
```

## 遍历数据

使用<code>keys、values、entries</code>都可以返回可遍历的迭代对象

```javascript
let tc = new Map([
  ['tc', 'tough.c'],
  ['zh', 'zh-CN'],
])

console.log([...tc.keys()].forEach(item => console.log(item))) // {'tc', 'zh'}
console.log(tc.values()) // {'tough.c', 'zh-CN'}
console.log(tc.entries()) // {'tc' => 'tough.c', 'zh' => 'zh-CN'}
```

使用<code>keys</code>和<code>values</code>遍历键和值

```javascript
let tc = new Map([
  ['tc', 'tough.c'],
  ['zh', 'zh-CN'],
])

for (let key of tc.keys()) {
  console.log(key)
}

for (let value of tc.values()) {
  console.log(value)
}
```

使用<code>for...of</code>遍历操作Map，等同于使用<code>entries</code>方法

```javascript
let tc = new Map([
  ['tc', 'tough.c'],
  ['zh', 'zh-CN'],
])

for (let [key, value] of tc) {
  console.log(key, value)
}

for (let [key, value] of tc.entries()) {
  console.log(key, value)
}
```

使用<code>forEach</code>遍历操作

```javascript
let tc = new Map([
  ['tc', 'tough.c'],
  ['zh', 'zh-CN'],
])

tc.forEach((value, key) => {
  console.log(`${key} => ${value}`)
})
```

## 数组转换

可以使用<code>...</code>延展运算法或<code>Array.from</code>将Map转为数组

```javascript
let tc = new Map([
  ['tc', 'tough.c'],
  ['zh', 'zh-CN'],
])

console.log(...tc) // ['tc', 'tough.c'] ['zh', 'zh-CN']
console.log(Array.from(tc)) // 
console.log(...tc.keys()) // tc zh
console.log(...tc.values()) // tough.c zh-CN
```
