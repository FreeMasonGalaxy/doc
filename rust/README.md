### 规则

+ 函数和变量名使用 `snake case` 规范风格
  
+ [Rust 是一门基于`表达式`（expression-based）的语言，这是一个需要理解的（不同于其他语言）重要区别](https://learnku.com/docs/rust-lang/2018/ch03-03-how-functions-work/4501)
  
  语句（Statements）是执行一些操作但不返回值的指令(如申明变量`let a: i32 = 1;`)，表达式（Expressions）计算并产生一个值

+ 

### 变量
>格式：关键字 [mut] 变量名 [:类型] = 值
>变量默认是不可改变的

关键字 `let`，可变性加 `mut`，可重复申明(隐藏)

```rust
let a: i32 = 123_0000; 
let mut b: i32 = 123_0000;  // 可变性
b = 234_0000;
let b: &str = "123_0000"; // 重复申明，覆盖之前的申明
```



### 常量
>格式：关键字 常量名 [:类型] = 值
> 常量名大写模式

关键字 `const`

```rust
const MAX_AGE:i32 = 200;

```

### 类型(数据类型)
>标量类型、复合类型

##### 标量类型(基本类型)

整型、浮点型、布尔类型和字符类型

```rust
8-bit	i8	u8
16-bit	i16	u16
32-bit	i32	u32
64-bit	i64	u64
arch	isize	usize

f32 f64
```

##### 复合类型
>元组、数组

```rust
let tup: (i32, f64, &str) = (500, 6.4, "test"); // 元组
let (x, y, z) = tup;
println!("元组子元素：{}",tup.0);

let a = [1, 2, 3, 4, 5]; // 数组，类型相同且长度不可变
let i = 1;
println!("数组子元素：{}",tup[i]);

```


### 函数

```rust
fn another_function(x: i32,y: i32) {
    println!("Another function.");
}

```

### 作用域
>`{}` 代码块，大括号也是一个表达式
```rust
let y = {
    let x = 3;
    let x1 = 2;
    
    x1 + x 
};
println!("{}",y); // 打印结果：5
```

### 流程控制
>根据条件是否为真来决定是否执行某些代码

##### 判断
>有一种：`if`

```rust
let cnd = 10;
if cnd % 2 == 0 {
    println!("if:{}",true);
}else if cnd % 5 == 0 {
    println!("if:{}",false);
}

let cnd = if cnd > 1 {

}

```

##### 循环
>有三种循环：loop、while、`for`

```rust

// for 使用的最多的
let arr = [10,20,30];
for ele in arr.iter() {
    println!("{}",ele)
}
for v in (1..10).rev() {
    println!("forr:{}",v)
}

// loop 关键字告诉 Rust 一遍又一遍地执行一段代码直到你明确要求停止
let mut  i = 0;
let f = loop {
    i+=1;
    if i > 100 {
        break i+100
    }
};
println!("f:{}",f);

// while 当条件为真，执行循环。当条件不再为真，调用 break 停止循环。这个循环类型可以通过组合 loop、if、else 和 break 来实现
let mut i = 100;
while i != 0 {
    i-=1;
};
println!("i:{}",i);

```

### 结构体
> 结构体、元组结构体、字段、方法、关联函数(构造函数)

关键字 `struct`

```rust
 // 结构体
#[derive(Debug)]
struct User<'b> {
    username: &'b str,
    email: String,
    age: i32,
    gender: bool,
    sign_in_count:u64,
}
// 实例化
let u = User {
    username: "kevin",
    // email: "test@test.com".to_string(),
    email: String::from("test"),
    age: 18,
    gender: true,
    sign_in_count: 1,
};
println!("u:{:#?}",u);

// 元组结构体
struct Color(i32, i32, i32);
#[derive(Debug)]
struct Point(i32, i32, i32);
let bk = Color(1, 2, 3);
let pt = Point(bk.0,0,0);
println!("{:#?}",pt);

// 更新结构体 u2
let u2 = User {
    email: String::from("another@example.com"),
    username: "anotherusername567",
    ..u
};

println!("u2:{:#?}",u2);

fn build_user(email: String, username: &str) -> User {
    User {
        email: email.parse().unwrap(),
        age: 0,
        username,
        sign_in_count: 1,
        gender: false,
    }
}

println!("fn-u:{:#?}",build_user(String::from("mail@com"), "test"));

```

##### 方法

```rust
// 结构体
#[derive(Debug)]
struct Rectangle {
    w: i32,
    h: i32,
}

impl Rectangle {
    // 方法
    fn area(&self) -> i32 {
        self.w * self.h
    }
    fn sum(&self) -> i32 {
        self.w + self.h
    }
}
impl Rectangle {
    // 只读
    // `&self` 跟 `rectangle: &Rectangle` 效果一样
    // 
    // 读写
    // 如果想要在方法中改变调用方法的实例，需要将第一个参数改为 &mut self
    fn sub(&mut self) -> i32 {
        self.w - self.h
    }
}
let r = Rectangle {
    w: 30,
    h: 50,
};
let mut r1 = Rectangle {
    w: 0,
    h: 100,
};
println!("rectangle:{} {} {}",r.area(),r.sum(),r1.sub(10));

```

##### 关联函数(构造方法)
```rust
#[derive(Debug)]
struct Rectangle {
    width: u32,
    height: u32,
}

impl Rectangle {
    fn square(size: u32) -> Rectangle {
        Rectangle { width: size, height: size }
    }
}
```


### 枚举