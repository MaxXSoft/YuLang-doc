# 4.3. when

`when` 语句用来表示多路的分支结构, 类似于其他语言中的 `switch` 语句.

`when` 也可以作为表达式使用, 前提条件和 `if-else` 类似:

1. `when` 语句内必须包含 `else` 分支;
2. `when` 语句内, 各分支对应的语句块的返回值类型必须一致.

`when` 表达式返回一个左值, 当且仅当其中所有分支对应的语句块都返回左值.

```yu
import io

extern def main(argc: i32, argv: u8**): i32 {
  var num: i32
  out <<< "input a number: "
  iin >>> num

  // `when` 作为表达式使用
  out <<< when num {
            0 { "zero!" }
            1 { "one!" }
            2, 3, 4, 5 { "2 to 5" }
            6 { "my lucky number" }
            else { "other numbers" }
          } <<< '\n'

  0
}
```
