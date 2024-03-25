不同于[[可访问性 - Accessibility]]，以下的可访问性是通过 @Environment 提供的。

## Differentiate Without Color

要使用它，只需添加以下环境属性：

```swift
@Environment(\.accessibilityDifferentiateWithoutColor) var differentiateWithoutColor
```

这个属性将是一个布尔值，可以据此来调整用户界面：

```swift
HStack {
            if differentiateWithoutColor {
                Image(systemName: "checkmark.circle")
            }
            Text("Success")
        }
        .background(differentiateWithoutColor ? .black : .green)

// 启用 "无色区分" 时，使用黑色背景和添加复选标记
```

## Reduce Motion

这意味着当涉及移动时，应限制 `withAnimation()` 的使用：

```swift
struct ContentView: View {
    @Environment(\.accessibilityReduceMotion) var reduceMotion
    @State private var scale = 1.0

    var body: some View {
        Button("Hello, World!") {
            if reduceMotion {
                scale *= 1.5
            } else {
                withAnimation {
                    scale *= 1.5
                }
            }

        }
        .scaleEffect(scale)
    }
}
```

但上文的用法会相当繁琐，以下是一个更简单的方法。使用这种方法，无需每次都重复动画代码。

1. 在 `withAnimation()` 周围添加一个小封装函数：

```swift
func withOptionalAnimation<Result>(_ animation: Animation? = .default, _ body: () throws -> Result) rethrows -> Result {
    if UIAccessibility.isReduceMotionEnabled {
        return try body()
    } else {
        return try withAnimation(animation, body)
    }
}
```

2. 在需要使用 `withAnimation()` 的地方使用该函数：

```swift
struct ContentView: View {
    @State private var scale = 1.0

    var body: some View {
        Button("Hello, World!") {
            withOptionalAnimation {
                scale *= 1.5
            }

        }
        .scaleEffect(scale)
    }
}
```

## Reduce Transparency

启用该选项后，应用程序应减少设计中使用的**模糊**和**半透明**程度，以确保一切都加倍清晰：

```swift
struct ContentView: View {
    @Environment(\.accessibilityReduceTransparency) var reduceTransparency

    var body: some View {
        Text("Hello, World!")
            .padding()
            .background(reduceTransparency ? .black : .black.opacity(0.5))
            .foregroundStyle(.white)
            .clipShape(.capsule)
    }
}

// 启用 "降低透明度" 时，此代码使用纯黑色背景，否则使用 50% 透明度
```

## VoiceOver

该环境属性用于告知 VoiceOver 是否被开启：

```swift
@Environment(\.accessibilityVoiceOverEnabled) var accessibilityVoiceOverEnabled
```

#swiftui 