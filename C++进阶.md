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



### 字符串函数



### 容器操作函数

别再像猴子一样叽叽喳喳乱喊乱叫.jpg

#### 赋值

| 函数       | 说明     |
| ---------- | -------- |
| fill       | 常数赋值 |
| fill_n     | 设定长度 |
| generate   | 函数赋值 |
| generate_n | 设定长度 |

#### 拷贝

| 函数 | 说明 |
| ---- | ---- |
| copy |      |
|      |      |
|      |      |
|      |      |
|      |      |

#### 排序

都需要容器的随机访问支持

| 函数             | 说明                          |
| ---------------- | ----------------------------- |
| sort             | 快排                          |
| stable_sort      | 稳定（归并）                  |
| partial_sort     | 堆排序 挑选出最小的若干个元素 |
| nth_element      | 只排出第n个元素               |
| is_sorted        | 检查是否有序                  |
| merge            | 合并                          |
| inplace_merge    | 就地合并                      |
| partition        | 就地分组                      |
| stable_partition | 稳定（就地分组）              |
| partition_copy   | 拷贝分组                      |
| partition_point  | 找出分组点                    |



#### 查找

| 函数 | 说明 |
| ---- | ---- |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |
|      |      |

#### 移动

advance

prev

copy

equal

#### 组合数

| 函数 | 说明 |
| ---- | ---- |
|      |      |
|      |      |
|      |      |
|      |      |

#### 堆

| 函数      | 说明 |
| --------- | ---- |
| make_heap |      |
| push_heap |      |
| pop_heap  |      |
| sort_heap |      |

### 内存操作函数

iota<!--名字来自APL语言，为小写希腊字母⍳，是物理上最小的字母，也指非常小的粒子或量-->

#### mem<cstring>

memcpy

memmove<!--当两地址区间有重叠时仍能正常工作-->

memset 

memchr

memcmp

#### str<cstring>

针对C风格字符串，遇到'\0'结束。

除非是接驳历史代码，否则绝对不要用。

strcat

strcmp

strcpy

strlen

strchr

strcspn

strdup

strrev

strstr

#### 申请&释放

new-delete

new[]-delete[]

malloc-free



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

**bit_cast< new_type >(expression)**

允许在编译阶段就确定类型。

顾名思义，按照bit重新识别类型。

**const_cast< new_type >(expression)**

解除const、volatile修饰符。



## 类型退化

## range

## coroutine

## module

## concept

## 智能指针