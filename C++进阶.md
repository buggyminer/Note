# C++进阶

## lamda演算

λ<变量>.<表达式>

(λ<变量>.<表达式>)<变量>

(λ<变量1,变量2>.<表达式>)<变量1,变量2>



### lamda表达式







### 图灵停机问题

*不存在这样一个程序（算法），它能够计算任何程序（算法）在给定输入上是否会结束（停机）。*

### y组合子







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



## 类型转换

**static_cast< new_type >(expression)**
**dynamic_cast< new_type >(expression)**