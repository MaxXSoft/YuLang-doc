# 3.3. 其他修饰符

你可以使用 `T[n]` 表示数组, 详见 [2.3 节](primitives/arrays.md).

你可以使用 `volatile` 后缀来标记类型, 编译器将不会试图消除对这类变量的内存访问. 这在嵌入式开发中十分有用, 比如用 `volatile` 指针来进行 MMIO 操作:

```yu
let led = 0x20001200 as i32 volatile var*
(*led) = 0b11001011
```

你可以使用 `(T1, T2, ...): Tret` 来表示一个函数的类型, 函数参数的类型为 `T1, T2, ...`, 返回值类型为 `Tret`. 具备该类型的变量可以指向一个相同类型的函数:

```yu
import io

def add(x: i32, y: i32): i32 {
  x + y
}

def print42() {
  out <<< 42 <<< '\n'
}

extern def main(argc: i32, argv: u8**): i32 {
  // `func1` 可指向一个具备两个 `i32` 类型参数, 返回值类型为 `i32` 的函数
  // 此时, `func1` 指向函数 `add`
  let func1: (i32, i32): i32 = add

  // 可以像调用普通函数一样调用 `func1`
  out <<< "1 + 2 = " <<< func1(1, 2) <<< '\n'

  // `func2` 可指向一个不具备参数, 且没有返回值的函数
  // 此时, `func2` 指向函数 `print42`
  let func2: () = print42
  func2()

  0
}
```

关于如何定义函数, 请参考 [5.1 节](def-funcs/def-decl.md).
