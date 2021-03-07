# 5.2. 参数和返回值

函数名称之后的括号内, 书写的是函数的参数列表, 其中包括了用逗号分隔的函数形参.

形参的记法和变量声明类似, 首先是参数名, 然后是冒号, 接着写参数的类型. 参数类型可以是包括数组, 指针, 引用在内的一切类型标记.

函数的参数列表后可以写一个冒号, 后跟函数的返回值类型. 如果函数不返回任何值, 其返回值类型应当留空.

```yu
import io

// 函数的两个参数分别为 `i32` 的可变引用类型, 以及 `i32` 类型
// 函数不会返回任何值
def plusX(n: i32 var&, x: i32) {
  n += x
}

extern def main(argc: i32, argv: u8**): i32 {
  var num = 10
  plusX(num, 233)
  out <<< "num = " <<< num <<< '\n'
  0
}
```