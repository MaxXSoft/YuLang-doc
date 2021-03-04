# 1.1. 从源代码构建

要使用羽语言编程, 你必须首先获取羽语言的编译器: `yuc`. 目前 `yuc` 并不提供任何预编译版本, 所以你需要从源代码构建羽语言的编译器.

请首先确保你的开发环境中安装了 `git`, `cmake`, `llvm` 8.0+, 以及支持 C++17 的 C++ 编译器 (建议使用 `g++` 或 `clang++`), 然后执行如下命令:

```
$ git clone --recursive https://github.com/MaxXSoft/YuLang.git
$ cd YuLang
$ mkdir build
$ cd build
$ cmake .. && make -j8
```

执行完毕后, 你的开发环境中会出现 `YuLang` 目录, 其中的 `build` 目录中包含了构建完毕的羽语言编译器 `yuc`, 羽语言的标准库 `libyu.a` 以及一些示例程序 (位于 `build/examples` 目录中).

运行 `yuc -v` 可查看版本信息, `yuc -h` 可查看编译器所支持的命令行参数, 详情如下:

```
$ ./yuc -h
Usage: yuc <INPUT> [OPTIONS...]

Arguments:
  input                         input source file

Options:
  -h, --help                    show this message
  -v, --version                 show version info
  -ot, --outtype <ARG>          type of output (ast/yuir/llvm/asm/obj)
  -o, --output <ARG>            output file, default to stdout
  -I, --imppath <ARG>           add directory to import search path
  -O, --opt-level <ARG>         set optimization level (0-3)
  -V, --verbose                 use verbose output
  -Werror, --warn-error         treat warnings as errors
  -tt, --target <ARG>           specify target triple
  -tc, --cpu <ARG>              specify target CPU
  -tf, --features <ARG>         specify target features
```
