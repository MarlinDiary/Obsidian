我们提前告诉视图 "如果有人想让您动态化，您应该这样回应"，仅此而已。

只需要在相应的组件后加上 [[修改器 - Modifier]] 即可：

```swift
.animation(.default, value: animationAmount)
```

隐式动画会对视图中发生变化的所有属性生效。

## 控制动画的类型

| 类型 | 效果 |
| ---- | ---- |
| .linear | 以恒定的速度移动 |
| .bouncy | 产生一个轻微弹跳的弹簧 |
| .spring(duration: 1, bounce: 0.9) | 可控制弹簧完成的大致时间，也可控制弹簧的弹跳程度 |
| .easeInOut(duration: 2) | 缓入缓出 |
| nil | 完全禁用动画 |

## 修改器

当我们说 `.easeInOut(duration: 2)` 时，实际上是在创建一个 `Animation` [[结构 - Struct]] 的实例，该结构拥有自己的 [[修改器 - Modifier]] 集。因此，可以将修改器直接附加到动画中：

```swift
.animation(
    .easeInOut(duration: 2)
        .delay(1),
    value: animationAmount
)
```

| 修饰符 | 作用 |
| ---- | ---- |
| .delay(1) | 动画效果延迟 1 秒 |
| .repeatCount(3, autoreverses: true) | 要求动画重复一定次数 |
| .repeatForever(autoreverses: true) | 可和 [[启动运行 - onAppear\|onAppear]] 结合，可类比为打关键帧 |

#animation #hard 