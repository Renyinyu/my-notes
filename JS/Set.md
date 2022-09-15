# Set

用于存储任何类型的唯一值，无论是基本类型或是引用类型

* 只有值，没有键名
* 严格类型检测（如字符串数字不等于数值数字）
* 值是唯一的（可用于去重）
* 遍历顺序是添加的顺序，方便保存回调函数

## 基本使用

对象的属性最终都会变为字符串

```javascript
let obj = { 1: 'tough.c', '1': 'tc'}
console.table(obj); // { 1: 'tc' }
```

用对象作为键时，会将对象转为字符串后使用

```javascript
let obj = { 1: 'tough.c', '1': 'tc'}

let tc = { [obj]: 'bbq' }
console.table(tc)

console.log(hd[obj.toString()]);
console.log(hd["[object Object]"]);
```

使用数组作为初始值

```javascript
let tc = new Set(['tough.c', 'tc.com'])
console.log(tc.values()); // SetIterator {'tough.c', 'tc.com'}
```

Set中是严格类型约束，下面的"1"和1属于两个不同的值
```javascript
let tc = new Set(['1', 1])
console.log(tc) // Set(2) {'1', 1}
```

使用<code>add</code>添加元素，重复添加相同的值会被过滤

```javascript
let tc = new Set()

tc.add('tough.c')
tc.add('tough.c')
tc.add('tough.c222')
console.log(tc) // Set(2) {'tough.c', 'tough.c222'}
```

## 获取数量

获取元素数量

```javascript
let tc = new Set()

tc.add('tough.c')
tc.add('tough.c')
tc.add('tough.c222')
console.log(tc.size) // 2
```

## 元素检测

检测元素是否存在集合中

```javascript
let tc = new Set()

tc.add('tough.c')
tc.add('tough.c')
tc.add('tough.c222')
console.log(tc.has('tough.c')) // true
```

## 删除元素

使用<code>delete</code>方法删除单个元素，返回值为<code>boolean</code>类型

```javascript
let tc = new Set()

tc.add('tough.c')
tc.add('tough.c222')

console.log(tc.delete('tough.c')) // true
console.log(tc.values()) // SetIterator {'tough.c222'}
console.log(tc.has('tough.c')) // false
```

使用<code>clear</code>删除所有元素

```javascript
let tc = new Set()
tc.add('tough.c')
tc.add('tough.c222')

tc.clear()
console.log(tc.values()) // {}
```

## 数组转换

可以使用<code>延展运算法(...)</code> 或 <code>Array.from</code> 将Set转成数组

```javascript
let set = new Set(['tough.c', 'houseilei'])
console.log([...set]) // ['tough.c', 'houseilei']
console.log(Array.from(set)) // ['tough.c', 'houseilei']
```

移除Set中大于5的数值

```javascript
let set = new Set(["123456789"])
set = new Set([...set].filter(item => item <= 5))
```

## 去重

字符串去重

```javascript
new Set('aaabbbbcccddd'.split('')) // {a, b, c, d}
```

数组去重

```javascript
new Set([1,1,1,1,13,3,2,3,2,32,3,2])
```


## 遍历数据

使用<code>keys()/values()/entries()</code>都可以返回可迭代对象，因为<code>set</code>只有值所以<code>keys和values()</code>方法结果一致

```javascript
let tc = new Set(['tough.c', 'tc'])

console.log(tc.values())
console.log(tc.keys())
console.log(tc.entries())
```

可以使用<code>forEach</code>遍历Set数据，默认使用<code>values</code>创建迭代器

```javascript
let set = new Set([1,2,3,4,5,6])

set.forEach((item, key) => console.log(item, key))
```

也可以使用<code>for...of</code>遍历Set数据，默认使用<code>values</code>创建迭代器

```javascript
let set = new Set([1,2,3,4,5,6])

for (const itor of set) {
  console.log(itor)
}
```

## 交集

获取两个集合中共同存在的元素

```javascript
const set1 = new Set(['tough.c', '123'])
const set2 = new Set(['tough.c', '1'])

const newSet = new Set([...set1].filter(item => set2.has(item)))

console.log(newSet) // Set(1) {'tough.c'}
```

## 并集

将两个集合合并成一个新的集合，由于Set的特性不会产生重复元素

```javascript
const set1 = new Set(['tough.c', '123'])
const set2 = new Set(['tough.c', '1'])
const newSet = [...set1, ...set2]
```

## 差集

在集合a中出现但在集合b中出现集合

```javascript
const set1 = new Set(['tough.c', '123'])
const set2 = new Set(['tough.c', '1'])

const newSet = new Set([...set1].filter(item => !set2.has(item))) // ['123']
```
