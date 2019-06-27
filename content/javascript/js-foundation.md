## javascript-foundation
### prototype简介
> 每个函数都有一个prototype属性，这个属性是指向一个对象的引用，这个对象称为原型对象，原型对象包含函数实例共享的方法和属性，也就是说将函数用作构造函数调用（使用new操作符调用）的时候，新创建的对象会从原型对象上继承属性和方法。
#### prototype,__proto__,constructor

```javascript
function Test() {}
console.log(Test.prototype) // 每个构造函数都有prototype属性，指向一个对象（由构造函数调用创建的实例的原型）
let test1 = new Test()
console.log(test1.__proto__) // __proto__该属性指向这个对象的原型
console.log(test1.__proto__===Test.prototype) // true 构造函数的prototype就是实例对象的__proto__
console.log(test1.__proto__.constructor===Test) // true 实例对象的原型有一个属性叫constructor，这个属性指向Test构造函数
console.log(Object.getPrototypeOf(test1) === Test.prototype) // true es5语法获取对象原型
console.log(test1.constructor === Test.prototype.constructor) // true
console.log(test1.constructor === Test) // 由于实例对象是没有constructor，所以回去找实例原型的constructor

```
#### 实例和原型的关系
> 当读取实例的属性时，如果找不到，就会查找与实例对象关联的原型中的属性，如果还查不到，就去找原型的原型，一直找到最顶层为止。

```javascript
// 读取实例属性的顺序 读取实例对象的属性 ---> 读取实例原型的属性 ---> 读取原型的原型的属性
function Test() {
	this.name = '1'
}
Object.prototype.name = '4'
Test.prototype.name = '2'
let test1 = new Test()
test1.name = '3'
console.log(test1.name) // 3

delete test1.name
console.log(test1.name) // 2
console.log(test1.__proto__)

delete Test.prototype.name
console.log(test1.name) // 4
console.log(test1.__proto__)

delete Object.prototype.name
console.log(test1.name) //undefined
console.log(test1.__proto__)
```

#### 原型的原型
> 其实原型对象就是通过 Object 构造函数生成的，结合之前所讲，实例的 __proto__ 指向构造函数的 prototype
原型的原型就是Object.prototype

#### 原型链
> 那 Object.prototype 的原型呢？

```javascript
console.log(Object.prototype.__proto__ === null) // true
```
> 所以 Object.prototype.__proto__ 的值为 null 跟 Object.prototype 没有原型，其实表达了一个意思。所以查找属性的时候查到 Object.prototype 就可以停止查找了。

`
原型链为：
实例对象.__proto__ ---> 实例原型（实例.prototype） 
实例原型.__proto__ ---> Object.prototype 
Object.prototype.__proto__ === null
`

#### __proto__
> 绝大部分浏览器都支持这个非标准的方法访问原型，然而它并不存在于 Person.prototype 中，实际上，它是来自于 Object.prototype ，与其说是一个属性，不如说是一个 getter/setter，当使用 obj.__proto__ 时，可以理解成返回了 Object.getPrototypeOf(obj)。