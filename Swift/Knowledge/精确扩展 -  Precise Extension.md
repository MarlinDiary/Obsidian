精确[[扩展 - Extension]]可以帮助我们实现以下效果：“**我们希望为 `ShapeStyle` 添加功能，但仅限于将其用作[[颜色 - Color]]的情况。**“

```swift
extension ShapeStyle where Self == Color {
    static var darkBackground: Color {
        Color(red: 0.1, green: 0.1, blue: 0.2)
    }

    static var lightBackground: Color {
        Color(red: 0.2, green: 0.2, blue: 0.3)
    }
}
```

这样便可以直接使用：

```swift
.background(.lightBackground)
```

#extension