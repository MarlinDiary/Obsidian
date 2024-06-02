## View 协议

该 [[协议 - Protocol]] 只有一个要求，即您必须拥有一个名为 `body` 的计算属性，并返回 `some View` 。

## some View 类型

其实，在明确知道类型的情况下，把 View 写成这样是完全合法的：

```swift
struct ContentView: View {
    var body: Text {
        Text("Hello, world!")
    }
}
```

但 `some View` 让我们可以说："这将是一个 View，如 `Button` 或 `Text` ，但我不想说是什么"。

以下是两种特殊情况：

1. 如果您创建了一个包含两个文本视图的 `VStack` ，SwiftUI 会静默地创建一个包含这两个视图的 `TupleView`；
2. 如果我们直接从 `body` 属性发送回两个视图，而不将它们封装在[[堆栈 - Stack]]中，Swift 将一个名为 `@ViewBuilder` 的特殊属性静默地应用于 `body` 属性。这样做的效果是在 `TupleView` 容器中静默地封装多个视图，这样，即使我们看起来发送回的是多个视图，它们也会合并为一个 `TupleView` 容器。

## Swift 用结构体表示视图的原因

1. 性能因素：[[结构 - Struct]]比[[类 - Class]]更简单、更快速；
2. 不可自由更改：它迫使我们考虑以一种简洁的方式隔离状态（[[属性包装器#@State]]）。

## 简化复杂的视图层次

方法之一：将视图创建为自己视图的属性，然后在布局中使用该属性。

```swift
struct ContentView: View {
    let motto1 = Text("Draco dormiens")
    let motto2 = Text("nunquam titillandus")

    var body: some View {
        VStack {
            motto1
            motto2
        }
    }
}
```

Swift 不允许我们创建一个指向其他存储属性的**存储属性**，如创建绑定到本地属性的 `TextField`。但如果你愿意，可以用[[结构 - Struct#计算属性 - Computed Property]]。

但要注意：与 `body` 属性不同，Swift 不会在**计算属性**处自动应用 `@ViewBuilder` 属性，因此如果您想发送多个视图，您有三种选择：

1. 使用 [[堆栈 - Stack]]；
2. 您也可以发送 `Group`；*（似乎没有特别的意义，只是用于打包）*
3. 第三种方法是自己添加 `@ViewBuilder` [[属性包装器]]。*（最佳选项，因为模仿了框架）*

```swift
@ViewBuilder var spells: some View {
    Text("Lumos")
    Text("Obliviate")
}
```

## 自定义组件

就是主动构造（封装）一个新的[[结构 - Struct]]：

```swift
struct CapsuleText: View {
    var text: String

    var body: some View {
        Text(text)
            .font(.largeTitle)
            .padding()
            .foregroundStyle(.white)
            .background(.blue)
            .clipShape(.capsule)
    }
}
```

在创建该 View 的实例时，我们就可以像这样应用自定义颜色：

```swift
VStack(spacing: 10) {
    CapsuleText(text: "First")
        .foregroundStyle(.white)
    CapsuleText(text: "Second")
        .foregroundStyle(.yellow)
}
```

之所以可以这样，是因为这些 [[修改器 - Modifier]] 本质上是 [[协议 - Protocol]] 的 [[扩展 - Extension]]，与我们自己创建的结构体无关。

## 原始视图

如果所有视图都是由其他视图组成的，那么它的终点究竟在哪里？

其中的诀窍就在于 Apple 所称的原始视图--SwiftUI 的绝对基本构件，它符合 `View` 但返回一些固定的内容，而不是呈现其他类型的视图。

这些构件有很多，而且并不令人感到惊讶，例如 `Text` 就是其中之一，还有 `Image` 、 `Color` 、 `Spacer` 等等。最终，我们构建的所有用户界面都是在这些构建模块的基础上创建的，这就是打破看似无限循环的原因所在。

#protocol #swiftui #struct #easy 