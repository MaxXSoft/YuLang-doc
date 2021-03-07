# 6.2. 定义枚举

你可以使用 `enum` 关键字定义一个枚举类型.

枚举类型本质上是整数类型, 枚举本质上是整数常量, 所以在定义枚举时, 你可以:

1. 在枚举类型的名称之后声明其实际的类型, 以约束一个枚举类型变量所占的大小;
2. 指定某个枚举所实际具备的整数数值.

```yu
import io

// 枚举默认使用 `i32` 类型存储
enum GameState {
  Scissors,
  Paper,
  Rock,
}

// 或者你可以指定枚举使用何种类型
enum GameResult : u32 {
  // 以及某个枚举的值
  // 枚举值的变换规则和 C/C++ 一致
  AliceWon,
  BobWon = 233 as u32,
  Draw,
}

def whosWinning(alice: GameState, bob: GameState): GameResult {
  if alice == bob {
    // 引用一个枚举时必须写明枚举属于哪一个枚举类型
    GameResult.Draw
  }
  else if (alice == GameState.Scissors && bob == GameState.Paper) ||
          (alice == GameState.Paper && bob == GameState.Rock) ||
          (alice == GameState.Rock && bob == GameState.Scissors) {
    GameResult.AliceWon
  }
  else {
    GameResult.BobWon
  }
}

extern def main(argc: i32, argv: u8**): i32 {
  let result = whosWinning(GameState.Rock, GameState.Paper)
  out <<< when result {
            GameResult.AliceWon { "alice won" }
            GameResult.BobWon { "bob won" }
            else { "draw" }
          } <<< '\n'
  0
}
```
