# 5.1. 定义和声明函数

你可以使用 `def` 关键字来定义函数:

```yu
import io

// 递归计算斐波那契数列第 n 项
def fib(n: i32): i32 {
  // 函数体的最后一个表达式将被作为函数的返回值
  if n <= 2 {
    1
  }
  else {
    fib(n - 1) + fib(n - 2)
  }
}

extern def main(argc: i32, argv: u8**): i32 {
  var n: i32
  out <<< "n = "
  iin >>> n

  // 调用 `fib` 函数
  out <<< "fib(n) = " <<< fib(n) <<< '\n'
  0
}
```

使用 `declare` 关键字声明一个已经定义的函数:

```yu
import io

// 声明 C 标准库中的 `atoi` 函数
// 由于羽语言的函数重载特性, 此处必须使用 `extern`
extern declare atoi: (u8*): i32

extern def main(argc: i32, argv: u8**): i32 {
  out <<< "atoi(\"42\") = " <<< atoi("42") <<< '\n'
  0
}
```

> 注: 关于 `extern` 的作用, 请参考 [7.1 节](modules/visibility.md?id=为什么需要-extern).
