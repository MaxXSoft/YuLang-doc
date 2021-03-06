# 4.2. if-else

`if-else` 语句用来表示分支结构.

羽语言中的 `if-else` 和其他语言中的类似, 区别是在羽语言中, `if-else` 可以作为表达式使用. 不过, 这么做的前提是:

1. `if` 和 `else` 必须同时出现, 不能只出现 `if` 而不出现 `else`;
2. `if` 和 `else` 对应的语句块的返回值类型必须一致.

`if-else` 表达式返回一个左值, 当且仅当 `if` 和 `else` 对应的语句块都返回左值.

```yu
import io
import sys.math

extern def main(argc: i32, argv: u8**): i32 {
  var score: i32
  out <<< "your score: "
  iin >>> score

  // 基本用法就像其他语言中的 if-else 一样
  if score >= 80 && score <= 100 {
    out <<< "excellent!\n"
  }
  else if score >= 60 && score < 80 {
    out <<< "good!\n"
  }
  else if score >= 0 && score < 60 {
    out <<< "unqualified.\n"
  }
  else {
    out <<< "invalid score!\n"
  }

  // 此外 if-else 可作为表达式使用
  let norm = if score >= 0 && score <= 100 {
               (sqrt(score as f64) * 10.0) as i32
             }
             else {
               score
             }
  out <<< "normalized score: " <<< norm <<< '\n'

  0
}
```
