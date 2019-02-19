# rust笔记

[工具](#工具)

[基础](#基础)

[基本概念](#基本概念)

[理解所有权](#理解所有权)

## 工具

### cargo: 编译工具及包管理工具

- cargo build: 编译项目
- cargo run: 运行项目
- cargo test: 测试项目
- cargo doc: 给项目生成文档
- cargo publish: 将lib发布到crates.io
- cargo new: 创建新项目 



### 安装格式化工具rustfmt以及链接工具clippy

```shell
rustup component add rustfmt
rustup component add clippy

# rustup操作
rustup update
rustup self uninstall
```



### 入门实例

```shell
# 创建项目目录
mkdir test1
# 进入目录新建main.rs代码源文件
touch main.rs
# 编写代码进行编译
rustc ./main.rs
```

```rust
fn main() {
    println!("this is a rust program!")
}
```

```shell
# cargo创建项目
cargo new cargo_test_20190209
cargo build/cargo check
cargo build --release
```

## 基础

使用标准库（standard library）

```rust
use std::io;
```

宏：!

定义变量

```rust
// rust中变量默认是不可变的
let a = 10
let mut b = 10 // 可变变量

// 关联函数（静态方法）
String::new()

// 异常捕获 io::Result => OK or Err
.expect()

// 打印宏占位符
println!("placeholder: {}", v);
```



## 基本概念

### 关键字

[具体了解](https://doc.rust-lang.org/book/appendix-01-keywords.html)



### 命名规范

两种方式：

- 第一个字符小写，剩下字符有数字、字母或_组成
- 第一个字符是_，但是必须大于一个字符，单独\_不能作为名字，剩下的可以用字母、数字或\_组成



### 原标识

有些场景下需要用到关键字或保留字，就可以使用原标识

```rust
let r#fn = "raw id"
r#match()
```



### 变量与可变性

**rust中变量默认不可变，这样提供了更高的安全性以及更简单的并发操作**

```rust
// 给变量绑定一个值
let a = 10
// 更改变量a的值
a = 8   // 将得到一下错误：cannot assign twice to immutable variable

// 声明可变变量
let mut x = 1
x = 6
```

#### 变量与常量的不同

- 常量不可用mut关键字
- 常量用const关键字定义，而且必须先声明常量类型
- 常量可以在任何作用域被定义
- 常量一般都是在常量表达式中被设置，不会是运行时赋计算或某个方法的返回值赋予

#### 变量影shadowing

同一变量名被多次声明，上一次的变量名被影化，值以最后一次为准

```rust
let x = 5;

let x = x + 1;

let x = x * 2;

// x的值为12
```

与mut的不同：

- 必须使用let，不然会有编译错误，可以改变值但完成后仍然是值不可变变量
- let会创建一个新变量，这样可以改变变量的数据类型但仍然使用相同的变量名



### 数据类型

**数据类型的子集：纯量和复合类型；rust是一门静态语言，所以编译的时候必须知道所有变量类型；**

#### 纯量类型：

**integers, float-point numbers, Booleans, characters**

##### 整型类型：

| 位数                    | 有符号  | 无符号  |
| ----------------------- | ------- | ------- |
| 8-bit                   | `i8`    | `u8`    |
| 16-bit                  | `i16`   | `u16`   |
| 32-bit                  | `i32`   | `u32`   |
| 64-bit                  | `i64`   | `u64`   |
| 128-bit                 | `i128`  | `u128`  |
| arch[机器的CPU架构决定] | `isize` | `usize` |

###### 整型字面量：

| 自面量                 | 实例          |
| ---------------------- | ------------- |
| Decimal(十进制)        | `98_222`      |
| Hex(十六进制)          | `0xff`        |
| Octal(八进制)          | `0o77`        |
| Binary(二进制)         | `0b1111_0000` |
| Byte (`u8` only)(字节) | `b'A'`        |

###### 整型溢出

在debug模式下编译，直接panic终止程序；

在release模式下编译，num - 2^n

##### 浮点数

f32和f64，默认f64

数字操作：+ - * / % [更多细节](https://doc.rust-lang.org/book/appendix-02-operators.html)

##### 布尔型

```rust
let t = true;
let f: bool = false;
```

*布尔型只占一个字节的大小*

##### 字符类型

```rust
let c = 'z';
let z = 'ℤ';
let heart_eyed_cat = '😻';
```

rust的char是unicode纯量值



#### 复合类型

##### 元组

```rust
let tup: (i32, f64, u8) = (500, 6.4, 1);
let (x, y, z) = tup;
let a = tup.0
let b = tup.1
let c = tup.2
```

##### 数组类型

与tuple不同的是数组所有元素的类型必须一样，但是与tuple一样都有固定长度

```rust
let a = [1, 2, 3, 4, 5];
// 定义数组长度为5且元素类型为32位有符号整型，
let b: [i32; 5] = [1, 2, 3, 4, 5];
```

数组是不能进行缩容或扩容，如果不了解具体元素数量，请使用vector

### 函数（方法）

**rust中所有的方法名或变量名都以下划线的方式命名，所有字母都小写，并且以下划线分割**

```rust
fn function_name() {
    // TODO
}
```

#### 参数

```rust
fn test_param(x: i32, y: u64) {
    
}
```

方法体包含了声明及表达式

#### 返回值

```rust
fn plus_one(x: i32) -> i32 {
    x + 1
}
```



### 控制流程

#### if 表达式

```rust
if bool {
   
} else if bool {
    
} else {
    
}
```

let声明中使用if

```rust
let number = if condition {
    5
} else {
    6
};
// if和else返回的类型必须一致
```

#### 循环

##### loop

```rust
loop {
    println!("again!");
}
let result = loop {
	counter += 1;

    if counter == 10 {
        break counter * 2;
    }
};
```

##### while

```rust
while number != 0 {
	println!("{}!", number);
	number = number - 1;
}
```

##### for

```rust
for element in array.iter() {
    println!("the value is: {}", element);
}
for number in (1..4).rev() {
    println!("{}!", number);
}
```



## 理解所有权

**所有权几乎是Rust的唯一特性，它能够不用垃圾回收来保证内存安全**



### 什么是所有权

Rust通过一组系统所有权的规则在编译时检查来管理内存，这并不会拖慢程序运行



#### 所有权规则

- 所有值在rust中都有一个被称为所有者的变量
- 同一时间只能有一个所有者
- 当所有者超出当前范围，只将被丢弃



#### 变量范围

##### string type

```rust
let s = String::from("test");
let mut ms = String::from("ok");
ms.push_str("a");

```

#### 内存与分配

就像上面支持可变、扩容的字符串类型，需要在堆上分配一大块内存

- 运行时操作系统需要分配内存 （程序员操作）
- 当使用完后需要一个方法将此内存返还操作系统 （当变量超出了自身范围就立即调用drop方法进行回收）



```rust
// 浅拷贝
let s1 = String::from("hello");
let s2 = s1;

println!("{}, world!", s1); // 异常，s1把不再验证

// 深拷贝
let s1 = String::from("hello");
let s2 = s1.clone();

println!("s1 = {}, s2 = {}", s1, s2);

// 编译时确定数据大小，只存于栈中
let x = 5;
let y = x;

println!("x = {}, y = {}", x, y);
```

### 引用与借用

```rust
fn main() {
    let s1 = String::from("hello");

    let len = calculate_length(&s1);

    println!("The length of '{}' is {}.", s1, len);
}

fn calculate_length(s: &String) -> usize {
    s.len()
}
// 借用的引用不可变
```

#### 可变的引用

```rust
fn main() {
    let mut s = String::from("hello");

    change(&mut s);
}

fn change(some_string: &mut String) {
    some_string.push_str(", world");
}
```

**有一个重要的限制：只能有一个可变变量在指定域引用到指定数据块**

这个限制的好处是禁止在编译时数据竞争，数据竞争出现在以下三种情形：

- 同一时间2个或多个指针访问统一数据
- 至少有一个指针会去对数据做写操作
- 访问数据时没有使用同步机制



### Slice



