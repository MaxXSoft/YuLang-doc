# 4.4. while

`while` 语句用来表示循环, 如果条件满足, 循环将一直进行下去.

```yu
import io

extern def main(argc: i32, argv: u8**): i32 {
  var n: i32
  out <<< "n = "
  iin >>> n

  // 计算斐波那契数列的第 n 项
  var last = 1, cur = 1
  while n > 2 {
    let temp = last
    last = cur
    cur += temp
    n -= 1
  }

  out <<< "fib(n) = " <<< cur <<< '\n'
  0
}
```
