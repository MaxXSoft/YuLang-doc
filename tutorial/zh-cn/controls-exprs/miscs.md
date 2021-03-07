# 4.6. 杂项

你可以使用 `break` 或 `continue` 来干涉 `while` 或 `for-in` 循环的执行过程:

* 使用 `break` 退出整个循环, 并继续执行循环之后的语句;
* 使用 `continue` 跳过当前循环, 并继续执行下一次循环.

```yu
import io

extern def main(argc: i32, argv: u8**): i32 {
  var i = 0

  // 这是一个无限循环
  while true {
    i += 1
    if i == 5 {
      // 跳过当前循环
      continue
    }

    out <<< "i = " <<< i <<< '\n'
    if i == 10 {
      // 退出整个循环
      break
    }
  }

  0
}
```

使用 `return` 提前从函数中返回:

```yu
import io
import range

extern def main(argc: i32, argv: u8**): i32 {
  // 必须提供命令行参数
  if argc < 2 {
    out <<< "usage: " <<< argv[0] <<< " <args...>\n"
    return 1
  }

  // 输出所有的命令行参数
  for i in 1 until argc {
    out <<< "arg[" <<< i <<< "] = " <<< argv[i] <<< '\n'
  }

  0
}
```

使用 `asm` 语句块来向羽语言文件中插入汇编:

```yu
import io

extern def main(argc: i32, argv: u8**): i32 {
  out <<< "Hello!\n"

  // 程序会在此触发调试器断点
  // (假如你使用的是 x86 处理器的话)
  asm { "int3" }

  out <<< "Bye!\n"

  0
}
```
