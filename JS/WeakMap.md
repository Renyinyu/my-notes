# WeakMap

WeakMap是一组键值对集合

* 键必须是对象
* WeakMap的键是弱应用，值是正常引用
* 垃圾回收不考虑WeakMap的键
* 因为WeakMap是弱引用，由于其它地方操作成员可能会不存在，所以不可进行<code>forEach</code>遍历等
* 也没有<code>keys、values、entries</code>等方法和<code>size</code>属性
* 当键的外部引用删除时，希望自动删除数据时使用<code>WeakMap</code>

## 垃圾回收

WakeMap的键对象不会增加引用计数器，如果一个对象不被引用了会自动删除。

* 下例当<code>tc</code>删除时内存即删除，因为WeakMap是若引用不会产生引用计数
* 当垃圾回收时因为对象被删除，这时WeakMap也就没有记录了

```javascript
let map = new WeakMap()
let tc = {}
map.set(tc, 'tough.c')
tc = null
console.log(map)

setInterval(() => {
  console.log(map);
}, 1000);
```
