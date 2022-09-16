# WeakSet

WeakSet结构同样不会存储重复的值，但它的成员必须是引用类型的值

* 垃圾回收不考虑WeakSet，即WeakSet不会阻止垃圾回收，对象不被引用时WeakSet会自动删除该对象

* WeakSet是弱引用，由于其它地方操作成员可能会不存在，所以不可以进行<code>forEach</code>等遍历操作，也没有<code>keys、values、entries</code>等方法和size属性

## 基本操作

```javascript
const tc = new WeakSet()

const arr = ['toughC']

// 添加
tc.add(arr)

//删除
tc.delete(arr)

// 检索判断
tc.has(arr)
```