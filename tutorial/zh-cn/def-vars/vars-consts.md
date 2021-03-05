# 3.1. 变量和常量

我们之前一直使用 `let` 定义 “变量”, 但实际上这么定义出来的 “变量” 并不可变:

```yu
let x: i32 = 1
x = 2           // 编译出错
```

`let` 所定义的量与 C/C++ 中的常量类似, 如果需要定义变量, 可以使用 `var`:

```yu
import io

extern def main(argc: i32, argv: u8**): i32 {
  // 使用 `let` 定义不可变的量
  let magic_number: i32 = 42

  // 在定义时可以省略类型声明, 羽语言编译器会自动推导变量的类型
  let magic_number_plus_1 = 42 + 1

  // 使用 `var` 定义可变的量, 定义时类型声明同样可以省略
  var ans = magic_number
  out <<< "ans = " <<< ans <<< '\n'
  ans += magic_number_plus_1
  out <<< "now, ans = " <<< ans <<< '\n'

  // `let` 定义的量必须具备初始值, 但 `var` 定义的量可以不必
  // 此时, 必须给出该变量的类型声明, 否则编译器将无法得知它的类型
  var ret_code: i32
  ret_code = ans * 2

  ret_code
}
```
