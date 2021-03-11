# 2.1. 基本类型

羽语言提供如下的基本类型:

* 有符号整数: `i8`, `i16`, `i32`, `i64`, `isize`, 分别代表 8 位, 16 位, 32 位, 64 位以及指针宽度的有符号整数.
* 无符号整数: `u8`, `u16`, `u32`, `u64`, 分别代表 8 位, 16 位, 32 位, 64 位以及指针宽度的无符号整数.
* 浮点数: `f32`, `f64` 分别代表单精度和双精度浮点数.
* 布尔类型: `bool`, 只具备 `true` 和 `false` 两种值.

此外, 你还可以使用 `type` 语句来指定类型的别名:

```yu
extern def main(argc: i32, argv: u8**): i32 {
  // 定义类型 `i32` 的别名为 `Int`
  type Int = i32

  // 定义一个类型为 `Int` 的常量
  let ret_code: Int = 0
  ret_code
}
```

如果要在基本类型之间进行类型转换, 你可以使用 `as`:

```yu
extern def main(argc: i32, argv: u8**): i32 {
  // 定义一个类型为 `i8` 的常量, 其值为命令行参数的个数
  let argc8: i8 = argc as i8

  // `main` 函数的返回值类型必须为 `i32`
  argc8 as i32
}
```

> 注: 羽语言几乎不支持任何形式的隐式类型转换, 这意味着你在大部分情况下都需要使用 `as` 进行手动的类型转换, 比如在两个不同位宽的整数之间执行加法运算时.

使用 `sizeof` 可以获得类型的大小:

```yu
extern def main(argc: i32, argv: u8**): i32 {
  // 获取 `i32` 类型的大小
  let sizeof_i32: usize = sizeof i32

  // 将其作为 `main` 的返回值
  sizeof_i32 as i32
}
```

> 注: `sizeof` 返回结果的类型为 `usize`
