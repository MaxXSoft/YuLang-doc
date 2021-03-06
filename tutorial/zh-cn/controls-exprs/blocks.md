# 4.1. 语句块

语句块是一组使用 `{}` 包裹的语句, 它是最简单的控制流: 其中的语句均按顺序执行; 同时, 它也可以和其他关键字组成更复杂的控制流.

在羽语言中, 语句块是可以作为表达式使用的. 语句块的值取决于语句块中最后一条语句/表达式的返回值. 如果最后一条语句/表达式返回了一个左值, 语句块的值也将是一个左值.

语句块中一行可以写多条语句, 此时, 语句之间需要使用 `;` 分隔.

```yu
import io

extern def main(argc: i32, argv: u8**): i32 {
  // 语句块和普通的表达式一样
  let x = {
    // 一行内的多条语句之间使用分号分隔
    var y = 10; y *= 10

    // 语句块的值即为 `y + 1`
    y + 1
  }

  // 输出 `x` 的值
  out <<< "x = " <<< x <<< '\n'

  // 无法输出 `y` 的值, 因为变量 `y` 是在语句块内定义的
  // out <<< "y = " <<< y <<< '\n'

  // 语句块可以返回左值
  var y = x
  { y *= 3; y } += 1
  out <<< "y = " <<< y <<< '\n'

  0
}
```
