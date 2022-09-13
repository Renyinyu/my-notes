# undefined/null

## undefined

对未声明但未赋值的变量返回类型为<code>undefined</code>表示变量未赋值

```javascript
  let hd;
  console.log(typeof hd); // undefined
```

访问未声明的变量会报错
```javascript
  console.log(typeof tc) // undefined
  tc // Uncaught ReferenceError: tc is not defined
```

函数参数或无返回值为<code>undefined</code>
```javascript
  function tc(web) {
    console.log(web) // undefined
  }
  console.log(tc()) // undefined
```

## null

<code>null</code>用于定义一个空对象；即如果变量要用来保存引用类型，可以在初始化时将其设置为<code>null</code>

```javascript
  let tc = null;
  console.log(typeof tc) // object
```