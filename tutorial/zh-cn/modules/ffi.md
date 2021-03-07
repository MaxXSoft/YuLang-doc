# 7.3. 和其他语言交互

通过使用 `extern` 修饰函数定义或声明, 羽语言可以为其他语言提供可调用的函数, 或者调用其他语言提供的函数.

## 为其他语言提供函数

模块 `hello.yu` 定义了函数 `hello`:

```yu
import io

extern def hello(name: u8*) {
  out <<< "Hello " <<< name <<< "!\n"
}
```

我们可在 C 语言中调用该函数:

```clike
void hello(const char *);

int main(int argc, const char *argv[]) {
  hello("Suzumiya Haruhi");
  return 0;
}
```

## 调用其他语言提供的函数

C 语言中定义了函数 `goodbye`:

```clike
#include <stdio.h>

void goodbye(const char *name) {
  printf("Goodbye %s!\n", name);
}
```

我们可以在羽语言中声明并使用该函数:

```yu
extern declare goodbye: (u8*)

extern def main(argc: i32, argv: u8**): i32 {
  goodbye("Nagato Yuki")
  0
}
```
