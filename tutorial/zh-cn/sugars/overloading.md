# 8.1. 重载

羽语言支持函数重载.

此外, 羽语言还支持双目运算符的运算符重载. 我们可以通过定义一个名字和运算符一致的函数, 来重载某个运算符.

```yu
import io

struct Vec2 {
  x: i32,
  y: i32,
}

struct Vec3 {
  x: i32,
  y: i32,
  z: i32,
}

// 创建一个二维向量
def newVec(x: i32, y: i32): Vec2 {
  [Vec2] {x, y}
}

// 创建一个三维向量
def newVec(x: i32, y: i32, z: i32): Vec3 {
  [Vec3] {x, y, z}
}

// 二维向量相加
def +(lhs: Vec2&, rhs: Vec2&): Vec2 {
  [Vec2] {lhs.x + rhs.x, lhs.y + rhs.y}
}

// 三维向量相加
def +(lhs: Vec3&, rhs: Vec3&): Vec3 {
  [Vec3] {lhs.x + rhs.x, lhs.y + rhs.y, lhs.z + rhs.z}
}

// 输出二维向量信息
def printVec(v: Vec2) {
  out <<< '(' <<< v.x <<< ", " <<< v.y <<< ')'
}

// 输出三维向量信息
def printVec(v: Vec3) {
  out <<< '(' <<< v.x <<< ", " <<< v.y <<< ", " <<< v.z <<< ')'
}

extern def main(argc: i32, argv: u8**): i32 {
  // 新建两个二维向量
  let vec2_1 = newVec(1, 2)
  let vec2_2 = newVec(8, 12)

  // 新建两个三维向量
  let vec3_1 = newVec(3, 4, 5)
  let vec3_2 = newVec(2, 12, 17)

  // 执行相加运算
  out <<< "vec2_1 + vec2_2 = "
  printVec(vec2_1 + vec2_2)
  out <<< '\n'
  out <<< "vec3_1 + vec3_2 = "
  printVec(vec3_1 + vec3_2)
  out <<< '\n'
  0
}
```
