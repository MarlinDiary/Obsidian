## Modifier 的顺序很重要

因为，每个修改器都会创建一个应用了该 Modifier 的新[[结构 - Struct]]，而不仅仅是在视图上设置一个属性。

最好的思考方式是想象 SwiftUI 在每个修改器之后都会渲染视图。

## 条件 Modifier

最简单的方式是使用[[三元条件运算符]]：

```swift
struct ContentView: View {
    @State private var useRedText = false

    var body: some View {
        Button("Hello World") {
            // flip the Boolean between true and false
            useRedText.toggle()            
        }
        .foregroundStyle(useRedText ? .red : .blue)
    }
}
```

有时，使用 `if` 语句是不可避免的，但在可能的情况下，最好使用三元运算符。

## 环境 Modifier

*许多* 修改器都可以应用于[[堆栈 - Stack|容器]]，这样我们就可以同时对许多视图应用相同的修改器：

```swift
VStack {
    Text("Gryffindor")
    Text("Hufflepuff")
    Text("Ravenclaw")
    Text("Slytherin")
}
.font(.title)
```

如果任何子视图覆盖了**相同**的修饰符，子视图的版本会优先使用。但常规 Modifier 不会覆盖，而是会叠加效果。

## 自制 Modifier

1. 创建一个符合 `ViewModifier` [[协议 - Protocol]]的新结构；
2. 创建一个名为 `body` 的方法；
3. 该方法接受任何 `Content`，并必须返回 `some View`。

```swift
struct Title: ViewModifier {
    func body(content: Content) -> some View {
        content
            .font(.largeTitle)
            .foregroundStyle(.white)
            .padding()
            .background(.blue)
            .clipShape(.rect(cornerRadius: 10))
    }
}
```

`Content` 是一个占位符类型（范型），代表你将要修改的[[视图 - View]]的类型。如果我们将函数签名改为`body(content: some View) -> some View`，则意味着它只能接受和返回相同类型的视图。这将大大限制`ViewModifier`的灵活性。

现在，我们可以将其与 `modifier()` 修改器一起使用：

```swift
Text("Hello World")
    .modifier(Title())
```

但在使用自定义修饰符时，通常明智的做法是在 `View` 上创建[[扩展 - Extension]]：

```swift
extension View {
    func titleStyle() -> some View {
        modifier(Title())
    }
}
```

也可以直接用扩展添加新方法，但相比之下，最大的弊端在于不可以有「**存储属性**」。

#struct #function #swiftui #condition 