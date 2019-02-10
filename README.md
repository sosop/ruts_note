# rust笔记

[工具](#工具)

[基础](#基础)

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

