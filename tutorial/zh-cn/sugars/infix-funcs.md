# 8.2. 中缀函数

在羽语言中, 任何对具备两个参数的函数的函数调用, 如 `func(x, y)`, 都可以被写作 `x func y`. 这种写法被称作 “中缀函数调用”, 而此时的 `func` 则可被称作一个 “中缀函数”.

中缀函数调用相比于其他操作, 如二元运算, 类型转换, 普通的函数调用而言, 优先级是最低的. 并且, 中缀函数调用具备左结合性, 也就是说 `x func y func z` 相当于 `(x func y) func z`.

```yu
import io

def add(x: i32, y: i32): i32 {
  x + y
}

def mult(x: i32, y: i32): i32 {
  x * y
}

extern def main(argc: i32, argv: u8**): i32 {
  out <<< "1 + 2 * 3 = " <<< 1 + 2 * 3 <<< '\n'
  out <<< "1 add 2 mult 3 = " <<< (1 add 2 mult 3) <<< '\n'
  0
}
```

前几章曾提及 `range` 库中的 `until` 操作, 它本质上就是一个中缀函数调用.

## 定义新的运算符

羽语言允许用户定义**完全**以特殊符号组成的标识符, 前提是不能和已有的运算符冲突. 比如:

```yu
import io

extern def main(argc: i32, argv: u8**): i32 {
  let ++ = 1
  out <<< ++ <<< '\n'
  0
}
```

这个特性看起来十分奇怪, 但如果你把它和中缀函数一起使用, 你就可以定义新的运算符了:

```yu
import io

struct CondOpHelper {
  cond: bool,
  tval: i32,
}

def ?(cond: bool, tval: i32): CondOpHelper {
  [CondOpHelper] {cond, tval}
}

def :(helper: CondOpHelper, fval: i32): i32 {
  if helper.cond {
    helper.tval
  }
  else {
    fval
  }
}

extern def main(argc: i32, argv: u8**): i32 {
  var num: i32
  out <<< "input a number: "
  iin >>> num

  // 羽语言中原本是不支持三目条件运算符的
  // 不过这里我们定义了一套可以返回 `i32` 的三目条件运算符
  let abs = num < 0 ? -num : num
  out <<< "abs(num) = " <<< abs <<< '\n'
  0
}
```

`io` 库中的流输出运算符 (`<<<`) 就是用类似的方法定义的. “新运算符” 的结合性和优先级符合中缀函数调用的相关规则.

允许用于定义新运算符的符号包括: `~!@#$%^&*-=+\|:<.>/?`.
