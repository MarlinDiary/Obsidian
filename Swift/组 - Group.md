 当你想对一组视图应用相同的[[修改器 - Modifier]]，但又不想因此而引入新的布局元素时，`Group`是一个理想的选择。例如，你可能想在多个视图上应用相同的字体样式或颜色，而不改变它们在父视图中的布局。

以下是一个包含三个文本视图的 Group：

```swift
struct UserView: View {
    var body: some View {
        Group {
            Text("Name: Paul")
            Text("Country: England")
            Text("Pets: Luna and Arya")
        }
        .font(.title)
    }
}
```

Group 具有透明布局的特性，即其内部视图的布局是由其父视图决定的，一个例子如下：

```swift
struct ContentView: View {
    @State private var layoutVertically = false

    var body: some View {
        Button {
            layoutVertically.toggle()
        } label: { 
            if layoutVertically {
                VStack {
                    UserView()
                }
            } else {
                HStack {
                    UserView()
                }
            }
        }
    }
}
```

以上这种条件布局相当常见，在编写可在多种设备尺寸下运行的代码时，经常会出现这种情况。对于设备的尺寸，苹果提供了一个非常简单的解决方案，称为 "_size classes_"，它以一种非常模糊的方式告诉我们视图有多少空间。之所以说非常模糊，是因为在横向和纵向中只提供了两个尺寸，“compact” 和 “regular”。一个例子如下：

```swift
struct ContentView: View {
    @Environment(\.horizontalSizeClass) var horizontalSizeClass

    var body: some View {
        if horizontalSizeClass == .compact {
            VStack {
                UserView()
            }
        } else {
            HStack {
                UserView()
            }
        }
    }
}
```

在[[堆栈 - Stack]]中只有一个视图且不需要任何参数的情况下，可以将视图的初始化器直接传递给 `VStack` 以缩短代码：

```swift
if sizeClass == .compact {
    VStack(content: UserView.init)
} else {
    HStack(content: UserView.init)
}
```

值得一提的是，SwiftUI 还提供了一个名为 [[自适应视图 - ViewThatFits]] 的视图，可以在一定程度上简化上述的条件布局。

#swiftui #easy 