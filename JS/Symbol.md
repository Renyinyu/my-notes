# Symbol

Symbol 用于防止属性名冲突而产生，比如向第三方对象添加属性时

Symbol 值是惟一的，独一无二的不会重复的

## 基础知识

### Symbol

```javascript
let tc = Symbol();
let edu = Symbol();
console.log(tc); // Symbol()
console.log(tc == edu); // false
```

Symbol 不可以添加属性

```javascript
let tc = Symbol();
tc.name = "tough.c";
console.log(tc.name); // undefined
```

### 描述参数

可传入字符串用于描述 Symbol，方便在控制台分辨 Symbol

```javascript
let tc = Symbol("toughC");
let edu = Symbol("test");

console.log(tc); // Symbol('toughC')
console.log(edu.toString()); // 'Symbol(test)'
```

传入相同的描述参数 Symbol 也是独立唯一的，因为参数只是描述。但使用<code>Symbol.for</code>则不会

```javascript
let tc = Symbol("toughC");
let edu = Symbol("toughC");
console.log(tc == edu); // false
```

使用<code>description</code>可以获取传入的描述参数

```javascript
const tc = Symbol("toughC");
console.log(tc.description); // toughC
```

### Symbol.for

根据描述获取 Symbol，如果不存在则新建一个 Symbol

- 使用 Symbol.for 会在系统中将 Symbol 登记
- 使用 Symbol 则不会登记

```javascript
let tc = Symbol.for("toughC");
let edu = Symbol.for("toughC");
console.log(tc == edu); // true
```

### Symbol.keyFor

<code>Symbol.keyFor</code>根据使用<code>Symbol.for</code>登记的<code>Symbol</code>返回描述，如果找不到返回 undefined

```javascript
let tc = Symbol.for("toughC");
console.log(Symbol.keyFor(tc)); // toughC

let edu = Symbol("edu");
console.log(Symbol.keyFor(edu)); // undefined
```

### 对象属性

Symbol 是独一无二的所以可以包装对象属性的唯一

- Symbol 声明和访问使用<code>[symbol]</code>(变量)形式操作
- 也不能使用<code>.</code>语法，因为<code>.</code>语法是操作字符串属性的

下面写法是错误的，因为会将<code>symbol</code>当成字符串<code>symbol</code>处理

```javascript
let symbol = Symbol("toughC");
let obj = {
  symbol: "tough",
};
```

正确写法

```javascript
let symbol = Symbol("toughC");
let obj = {
  [symbol]: "tough",
};
console.log(obj[symbol]);
```

## 实例操作

### 缓存操作

使用<code>Symbol</code>可以解决在保存数据时由于名称相同造成的耦合覆盖的问题

```javascript
class Cache {
  static data = {};

  static set(name, value) {
    this.data[name] = value;
  }

  static get(name) {
    return this.data[name];
  }
}

let user = {
  name: "toughC",
  key: Symbol("缓存"),
};

let cart = {
  name: "购物车",
  key: Symbol("购物车"),
};

Cache.set(user.key, user);
Cache.set(cart.key, cart);
console.log(Cache.get(user.key));
```

### 遍历属性

Symbol 不能使用<code>for/in</code>、<code>for/of</code>遍历操作

```javascript
let symbol = Symbol("toughC");
let obj = {
  name: "toughC.com",
  [symbol]: "toughC.com",
};

for (const key in obj) {
  console.log(key); //name
}

for (const key of Object.keys(obj)) {
  console.log(key); //name
}
```

可以使用<code>Object.getOwnPropertySymbols</code>获取所有<code>Symbol</code>属性

```javascript
for (const key of Object.getOwnPropertySymbols(obj)) {
  console.log(key);
}
```

也可以使用<code>Reflect.ownKeys(obj)</code>获取所有属性包括<code>Symbol</code>

```javascript
for (let key of Reflect.ownKeys(obj)) {
  console.log(key);
}
```

如果对象属性不想被遍历，可以使用<code>Symbol</code>保护，也可以用来做类的私有成员属性

```javascript
const site = Symbol("网站名称");

class User {
  constructor(name) {
    this[site] = "toughC";
    this.name = name;
  }

  getName() {
    return `${this[site]}-${this.name}`;
  }
}

const hd = new User("toughC");
console.log(hd.getName());
for (const key in hd) {
  console.log(key);
}
```
