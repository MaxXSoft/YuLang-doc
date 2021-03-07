# 7.2. 导入模块

在羽语言中, 一个羽语言源代码文件 (`.yu` 文件) 表示一个羽语言模块.

你可以使用 `import` 语句来导入一个模块. 羽语言编译器将会从 `-I` 选项指定的路径中搜索待导入的模块.

如果你需要导入的模块不在 `-I` 指定的路径 `dir` 中, 而是位于 `dir/dir1/dir2/module.yu`, 你需要使用:

```yu
import dir1.dir2.module
```

来导入这个模块.

## 示例

模块 `action.yu` 中定义了枚举 `Action`:

```yu
public enum Action {
  Up, Down, Left, Right,
}

public def toString(action: Action): u8* {
  when action {
    Action.Up    { "up" }
    Action.Down  { "down" }
    Action.Left  { "left" }
    Action.Right { "right" }
    else         { "unknown" }
  }
}
```

模块 `move.yu` 中定义了函数 `move`:

```yu
// 因为 `move` 函数是对其他模块可见的, 而其类型声明中又引用了模块 `action` 中的内容
// 所以此处需要将 `import` 语句设为 `public`, 以防其他模块在引用该模块时不知道 `Action` 的具体定义
public import action
import io

public def move(name: u8*, action: Action) {
  out <<< name <<< " moves " <<< toString(action) <<< ".\n"
}
```

模块 `main.yu` 中使用了前两个模块, 并且定义了 `main` 函数:

```yu
import move
import action

extern def main(argc: i32, argv: u8**): i32 {
  move("Hakurei Reimu", Action.Left)
  move("Kirisame Marisa", Action.Up)
  move("Izayoi Sakuya", Action.Right)
  move("Kochiya Sanae", Action.Down)
  0
}
```

将上述三个文件放在同一个目录, 然后在目录中使用如下的命令编译得到可执行文件:

```
$ $YU_HOME/yuc -I $YU_HOME/lib -I . action.yu -o action.o
$ $YU_HOME/yuc -I $YU_HOME/lib -I . move.yu -o move.o
$ $YU_HOME/yuc -I $YU_HOME/lib -I . main.yu -o main.o
$ clang -L$YU_HOME/build -lyu action.o move.o main.o -o move
$ ./move
Hakurei Reimu moves left.
Kirisame Marisa moves up.
Izayoi Sakuya moves right.
Kochiya Sanae moves down.
```
