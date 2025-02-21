SwiftUI 提供了四种渐变供我们使用，和[[颜色 - Color]]一样，它们中的大多数（前三种）也是可以在用户界面中绘制的 View，或者作为修改器的一部分使用（如 background）。

## 渐变的组成

1. 颜色 Array
2. 尺寸和方向
3. 渐变种类

## 线性渐变

例如，线性渐变是单向的，因此我们要为它提供这样的起点和终点：

```swift
LinearGradient(colors: [.white, .black], startPoint: .top, endPoint: .bottom)
```

我们还可以使用**渐变停止点**：

```swift
LinearGradient(stops: [
    Gradient.Stop(color: .white, location: 0.45),
    Gradient.Stop(color: .black, location: 0.55),
], startPoint: .top, endPoint: .bottom)
```

**提示**：Swift 知道我们要在这里创建渐变止点，因此作为快捷方式，我们可以像这样写 `.init` 而不是 `Gradient.Stop` ：

```swift
LinearGradient(stops: [
    .init(color: .white, location: 0.45),
    .init(color: .black, location: 0.55),
], startPoint: .top, endPoint: .bottom)
```

## 径向渐变

我们不需要指定方向，而是指定开始和结束半径，即颜色从圆心开始变化的距离和停止变化的距离。

```swift
RadialGradient(colors: [.blue, .black], center: .center, startRadius: 20, endRadius: 200)
```

## 角度渐变

这种渐变在一个圆周上循环使用颜色，而不是向外辐射。

```swift
AngularGradient(colors: [.red, .yellow, .green, .blue, .purple, .red], center: .center)
```

## .gradient

你无法对其进行任何控制，而且只能将其用作背景和前景样式，而不是单独的视图。

```swift
Text("Your content")
    .frame(maxWidth: .infinity, maxHeight: .infinity)
    .foregroundStyle(.white)
    .background(.red.gradient)
```

#swiftui #struct #array #easy 