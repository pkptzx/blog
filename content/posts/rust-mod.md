---
title: "Rust中的mod(模块)使用的五种方式"
date: 2022-09-28T18:57:58+08:00
draft: false
weight: 70
keywords: ["rust"]
description: "Rust中的mod(模块)使用的五种方式"
tags: ["rust"]
categories: ["rust"]
author: "码魂"
url: "2022/09/28/rust-mod"
---
rust中的mod(模块)在项目中使用是必不可少的,但有很多种使用方式,有些方式比较推荐,我们来看看这些使用方式.

方式一: 当前类中定义并实现
```rust
mod x {
    pub(crate) fn x(){
        println!("x");
    }
    pub mod y{
        pub fn y(){
            println!("y");
        }  
        pub fn yy(){
            //可以使用self(可省)表示当前模块
            self::y();
            //可以使用super表示上层模块
            super::x();
        }   
    }
}
fn main() {
    x::x();
    x::y::y();
    x::y::yy();
}

```

方式二:同级目录中存放mod模块文件,如`bar.rs`
```rust
// bar.rs
pub fn bar() {
    println!("bar");
}
// mian.rs
mod bar;
fn main() {
    bar::bar();
}
```

方式三:带有文件夹的mod,需要在文件夹中创建mod.rs.  
```rust
// 目录结构:
// ┌─main.rs
// └─serviecs
//    ├─user.rs
//    └─mod.rs
// user.rs
pub fn hello() {
    println!("hello : Hello world!");
}
// mod.rs
pub mod user;
// main.rs
mod services;
fn main() {
    services::user::get();
}
```

以下两种方式为不含有mod.js的方式.  
方式四:创建与文件夹同名的模块定义文件,也就是将mod.rs改名后提到外层. (如果实在不想建mod.js,推荐这个方式,对于中小项目而言,这样更一目了然) 
```rust
// 目录结构:
// ┌─main.rs
// ├─services
// │  └─user.rs
// └─services.rs
// user.rs
pub fn get(){
    println!("get user");
}
// services.rs
pub mod user;
// main.rs
mod services;
fn main() {
    services::user::get();
}
```

方式五:在使用时声明带有文件夹的模块,不推荐,显得臃肿,也不便于维护
```rust
// 目录结构:
// ┌─main.rs
// └─services
//    └─user.rs
// user.rs
pub fn get(){
    println!("get user");
}
// main.rs
mod services {
    pub mod user;
}
fn main() {
    services::user::get();
}
```



