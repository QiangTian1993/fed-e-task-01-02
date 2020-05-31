# 简答题

## 问题一

描述引用计数的工作原理和优缺点。

答：

- 工作原理：每一个对象都会被分配一个应用数，当它的引用增加时这个引用数就加一，引用减少时就减一。当引用数为 0 时就会被垃圾回收。
- 优点：可以立即进行回收
- 缺点：无法回收循环引用的对象，可能会比较耗资源

## 问题二

描述标记整理算法的工作流程

答：标记整理算法会进行两次遍历，第一次遍历会将内存中所有的活动对象进行标记，第二次变量会将会将标记的对象和未标记的对象进行空间整理形成一个连续的内存空间，然后会将未标记的对象进行回收

## 问题三

描述 V8 中新生代存储区垃圾回收的流程

答：新生代存储主要采用的标记整理算法和复制算法。它会将内存分为两个等分的空间 from 和 to，活动的对象会存储在 from 中，空闲的对象存储在 to 中。首页会在 from 中进行标记整理算法，然后将所有标记的对象复制到 to 中，再将 from 与 to 的空间进行互换，最后对 from 空间中所有的对象进行回收

## 问题四

描述标记增量算法在何时使用，及工作原理

答：标记增量算法主要在 v8 的老生代存储区使用，它会将标记算法分为几个小阶段与程序交叉运行

# 代码题 1

## 练习一

使用函数组合 fp.flowRight() 重新实现下面这个函数

```js
let isLastInStock = function (cars) {
	// 获取最后一条数据
	let last_car = fq.last(cars);
	// 获取最后一条数据的 in_stock 属性值
	return fp.prop("in_stock", last_car);
};
```

答：

```js
let isLastInStock = (cars) => fq.flowRight(fp.prop("in_sock"), fq.last(cars));
```

## 练习二

使用 fp.flowRight()、fp.prop()、和 fp.first() 获取第一个 car 的 name

```js
let name = fq.flowRight(fp.prop("name"), fq.first(cars));
```

## 练习三

使用帮助函数 \_average 重构 averageDollarValue，使用函数组合方式实现

```js
let _average = function (xs) {
	return fp.reduce(fp.add, 0, xs) / xs.length;
};

let averageDollarValue = function (cars) {
	let dollar_values = fp.map(function (car) {
		return car.dollar_value;
	}, cars);

	return _average(dollar_values);
};
```

答：

```js
let _average = fp.flowRight(
	_average,
	fp.map((car) => car.dollar_value, cars)
);
```

## 练习四

使用 flowRight 写一个 sanitizeNames() 函数

答：

```js
const sanitizeNames = (cars) =>
	fp.flowRight(
		_underscore,
		fp.toLocaleLowerCase,
		fp.map((car) => car.name)
	);
```

# 代码题 2

## 练习一

使用 fp.add(x,y) 和 fp.map(f,x) 创建一个能让 functor 里的值增加的函数 ex1

答：

```js
let ex1 = (maybe) => maybe.map((x) => fp.map((value) => f.add(value, 1), x));

ex1(maybe);
```

## 练习二

实现一个函数 ex2， 能够是用 fp.first 获取列表的第一个元素

答：

```js
let ex2 = (xs) => xs.map((x) => fp.first(x));

ex2(xs);
```

## 练习三

实现一个函数 ex3， 使用 safeProp 和 fp.first 找到 user 的名字的首字母

答：

```js
let ex3 = (x, o) => safeProp(o[x]).map((x) => fp.first(x));

ex3("name", user);
```

## 练习四

使用 MayBe 重写 ex4, 不要有 if 语句

```js
let ex4 = Maybe.of(n).map((x) => fp.parseInt(x));
```
