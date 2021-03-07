# 7.1. 可见性

任何在全局环境内的语句, 包括:

* 变量定义 (`var`)
* 常量定义 (`let`)
* 函数定义 (`def`)
* 函数声明 (`declare`)
* 类型别名定义 (`type`)
* 结构体类型定义 (`struct`)
* 枚举类型定义 (`enum`)
* 模块导入语句 (`import`)

它们之前都可以添加可见性标识. 可用的可见性标识有:

* 什么也不写: 该语句所代表的定义/声明只在当前模块内可见.
* `public`: 该语句所代表的定义/声明对其他模块可见. 适用于以上所有语句.
* `extern`: 该函数定义/声明对其他模块可见, 同时, 编译器不会对该函数进行名称修饰 (name mangling). 只适用于函数定义/声明.
* `inline`: 该语句所代表的定义/声明对其他模块可见, 同时, 编译器会尝试将该定义/声明内联 (inline) 到引用该定义的模块或表达式内. 只适用于变量/常量/函数定义.

## 为什么需要 extern

羽语言具备[函数重载](sugars/overloading.md)的特性, 而函数重载的实现方式, 是对所有的函数进行名称修饰 ([name mangling](https://en.wikipedia.org/wiki/Name_mangling)).

要实现函数重载, 就必须允许用户定义两个名称相同, 但参数类型不同的函数. 然而, 链接器并不允许一个目标文件内出现两个代表函数的同名符号, 所以编译器必须修改这两个函数的实际名称. 比如以下的羽语言函数:

```yu
def func(x: i32, y: u8*): bool {
  ...
}
```

编译后的名称实际为 `_$func_i32$pu8`.

但假如因为某种原因, 比如需要和 C 语言交互, 我们就不希望编译器进行这种操作, 此时我们就需要使用 `extern` 修饰相关的函数定义和声明. 这也是为什么在羽语言中, `main` 函数的定义前必须写 `extern` 而非 `public`.

此外, 使用 `extern` 修饰的函数依然可以参与函数重载, 比如:

```yu
import io

extern def hello() {
  out <<< "Hello world!\n"
}

def hello(name: u8*) {
  out <<< "Hello " <<< name <<< "!\n"
}

extern def main(argc: i32, argv: u8**): i32 {
  hello()
  hello("Madoka")
  0
}
```
