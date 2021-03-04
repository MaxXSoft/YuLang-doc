# 1.2. Hello World

以下是使用羽语言编写的一个简单的 Hello World 程序:

```
// 你可以使用双斜线来编写注释
/* 当然,
   你也可以写 C 语言风格的多行注释 */

// 使用 `import` 语句来导入模块
// `io` 模块包含了标准输入和标准输出, 你可以使用标准输出, 向控制台输出文本
import io

// 这是 `main` 函数, 和 C/C++ 类似, 所以括号里的参数也可以不写
extern def main(argc: i32, argv: u8**): i32 {
  // 使用 `<<<` 向标准输出传递字符串
  out <<< "Hello world!\n"

  // 这里是 `main` 函数的返回值, 因为我们希望程序正常退出, 所以写 0
  0
}
```

将其保存为 `hello.yu`, 然后执行以下命令, 将其编译为 `hello.o` 并链接为可执行文件 `hello`:

```
$ $YU_HOME/yuc -I $YU_HOME/lib hello.yu -o hello.o
$ clang -L$YU_HOME/build -lyu hello.o -o hello
$ ./hello
Hello world!
```

> 注 1: 假设你的 `YuLang` 目录位于 `$YU_HOME`.
>
> 注 2: 假设你使用 `clang`/`clang++` 作为 C/C++ 编译器.

我们在调用 `yuc` 时, 提供了如下的编译选项:

* `-I $YU_HOME/lib`: 指定 `yuc` 在此处查找需要被 `import` 的模块的源文件.
* `hello.yu`: 指定待编译的羽语言源文件.
* `-o hello.o`: 指定输出的文件.
