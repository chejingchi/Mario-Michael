# es6-es7
## es6 
### let
1. let命令和var命令类似，用于声明变量。let在es6中用于替代var。let命令声明的变量只在它声明的代码块中生效
```javascript
// 在for循环中，let设置循环变量的是一个父级作用域，循环体为子级作用域 
// 在for循环中，let声明的i每次循环都是一个新的i，不会对之前的i有影响，js引擎会记录上次遍历的i，并且在本轮遍历的时候根据上次的i进行运算
for(let i = 0; i < 5; i++) {
  let i = 'aaaa'
  console.log(i)
}

for(let i = 0; i < 5; i++) {
  i = 'aaaa'
  console.log(i)
}
```
2. let不会存在变量提升，let所声明的变量一定要在声明后使用否则就会报错
3. let声明的变量，在let声明之前使用是会报错 （ReferenceError） 这种现象叫暂时性死区，这也就意味着type of方法不是百分百不会报错的哦
4. 同一个变量名不允许重复声明

### 块级别作用域

### const
1. const实际上保证的，并不是变量的值不得改动，而是变量指向的那个内存地址所保存的数据不得改动。对于简单类型的数据（数值、字符串、布尔值），值就保存在变量指向的那个内存地址，因此等同于常量。但对于复合类型的数据（主要是对象和数组），变量指向的内存地址，保存的只是一个指向实际数据的指针，const只能保证这个指针是固定的（即总是指向另一个固定的地址），至于它指向的数据结构是不是可变的，就完全不能控制了。因此，将一个对象声明为常量必须非常小心。
2. 将对象冻结，应该使用Object.freeze方法
3. 冻结对象的终极方法
```javascript
var constantize = (obj) => {
  Object.freeze(obj);
  Object.keys(obj).forEach( (key, i) => {
    if ( typeof obj[key] === 'object' ) {
      constantize( obj[key] );
    }
  });
};
```
4. 顶层对象（有空了解下）
  let命令、const命令、class命令声明的全局变量，不属于顶层对象的属性。

### 解构
#### 数组解构
