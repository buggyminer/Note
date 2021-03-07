# C++进阶

## lamda演算

λ<变量>.<表达式>

(λ<变量>.<表达式>)<变量>

(λ<变量1,变量2>.<表达式>)<变量1,变量2>



### lamda表达式



```c++
[]()mutable throw->{}
```

[]:=,&,this

():parameter

mutable:const

throw:exception

->:return type

{}:function body

### 图灵停机问题

*不存在这样一个程序（算法），它能够计算任何程序（算法）在给定输入上是否会结束（停机）。*

这个问题有严格的数学证明，也可以由编程语言直观地进行证明。

### y组合子

在lamda系统中，一切都是lamda，也就是函数。

有一种函数叫高级函数，它接收一个函数，而后输出一个函数。

y组合子是一个特殊的高级函数，它接收一个函数，并返回其自调用的结果，即把一个非递归的函数变为递归。

用它可以实现匿名函数的递归。在实际中应用得很少，但是在理论上很重要，体现了lamda的图灵完备性。

```scheme
lambda f. (lambda x. (f(x x)) lambda x. (f(x x)))
```

```c++
[](f){[](x{f(x)[](x){f(x)}}}
```

```c++
const auto& y = [](const auto& f) {
	return [&](const auto& x) {
		return x(x);
	}([&](const auto& x) -> std::function<int(int)> {
		return f([&](const int& n) {
			return x(x)(n);
		});
	});
};
```

还有一种伪递归实现方式，很不优雅，但某种程度上易于理解。把函数自身当作参数在内部调用。

## 常用函数

itoa int转字符串

atoi字符串转int

swap 交换内容

auto [x, y, z] = struct 分解结构体成员

accumulate 累加函数

constexpr 将表达式放在预编译阶段翻译为常数

freopen输入重定向

reverse反转元素顺序

bitset位集





### 位运算

a >> b & 1 代表检查 a 的第 b 位是否为 1，有两种可能性 0 或者 1

a += 1 << b 代表将 a 的第 b 位设置为 1 (当第 b 位为 0 的时候适用)

__bulletin





### 内存操作函数

memcpy

copy

new

delete

malloc

free



## 可变参数

```c++
void fun(int num,...)
```

告知编译器该函数可接受若干个参数，根据第一个有名参数确定参数在堆栈中的位置，根据数据大小计算地址访问参数。





## 断言

assert

尽早暴露问题。这一机制只能在debug阶段使用，绝对不要在release阶段使用。拒绝防御式编程！

## 类型转换

**static_cast< new_type >(expression)**

不能用于不相关类型转换。

不会改变修饰符。

**dynamic_cast< new_type >(expression)**

类型安全，失败会返回NULL。

一般用于子类和基类之间虚函数表的操作。

**reinterpret_cast< new_type >(expression)**

强制转换，非常暴力。

要严格注意地址计算，因此可移植性差，可能产生随机值，最好别用。

**const_cast< new_type >(expression)**

解除const、volatile修饰符。

