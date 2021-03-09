# 10.1. 交叉编译选项

羽语言编译器 (`yuc`) 支持如下选项, 可指定编译生成的目标文件的目标三元组 ([target triple](https://clang.llvm.org/docs/CrossCompilation.html#target-triple)) 等信息:

* `-tt, --target <ARG>`: 指定目标三元组.
* `-tc, --cpu <ARG>`: 指定目标 CPU.
* `-tf, --features <ARG>`: 指定目标所具备的额外特性.

如果不指定上述内容, 羽语言编译器将生成适合于当前目标的目标文件.
