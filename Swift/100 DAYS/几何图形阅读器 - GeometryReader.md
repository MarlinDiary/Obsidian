## 用于视图的自适应大小

`GeometryReader` 是一个[[视图 - View]]，只不过在创建它时，我们会得到一个 `GeometryProxy` 对象供我们使用。这让我们可以查询环境：容器有多大？视图在什么位置？是否有任何安全区域嵌入？

在实际操作中，需要谨慎使用 `GeometryReader` ，因为它会自动展开以占据布局中的可用空间，然后将自己的内容与**左上角**对齐。

例如，可以制作一幅宽度为屏幕 80%、高度为 300 的图像：

```swift
GeometryReader { proxy in
    Image(.example)
        .resizable()
        .scaledToFit()
        .frame(width: proxy.size.width * 0.8, height: 300)
}

// 这里的 height 数据是可以删除的
```

与使用[[相对框架 - Relative Frame]]的不同之处在于，`containerRelativeFrame()` 对 "容器" 的定义非常苛刻，它可能是整个屏幕，可能是 `NavigationStack` ，可能是 `List` 或 `ScrollView` 等等，但它不会将 `HStack` 或 `VStack` 这样的[[堆栈 - Stack]]视为容器：

```swift
HStack {
    Text("IMPORTANT")
        .frame(width: 200)
        .background(.blue)

    Image(.example)
        .resizable()
        .scaledToFit()
        .containerRelativeFrame(.horizontal) { size, axis in
            size * 0.8
        }
}
```

如果想将 `GeometryReader` 中的视图居中，而不是与左上角对齐，可以添加第二个框架，使其充满容器的整个空间：

```swift
GeometryReader { proxy in
    Image(.example)
        .resizable()
        .scaledToFit()
        .frame(width: proxy.size.width * 0.8)
        .frame(width: proxy.size.width, height: proxy.size.height)
}
```

## 内含独立的框架和坐标系

`GeometryReader` 允许我们使用其**大小**和**坐标**来确定子视图的布局，这也是在 SwiftUI 中创建某些最出色效果的关键所在。

在使用 `GeometryReader` 时，应始终牢记 SwiftUI 的三步[[布局 - Layout]]系统：父视图为子视图提出大小，子视图使用该大小确定自己的大小，父视图使用该大小对子视图进行适当定位。

`GeometryReader` 有一个有趣的副作用，它会尽可能多地扩展和占用屏幕的可用空间，就像这样：

```swift
struct ContentView: View {
    var body: some View {
        VStack {
            GeometryReader { proxy in
                Text("Hello, World!")
                    .frame(width: proxy.size.width * 0.9, height: 40)
                    .background(.red)
            }

            Text("More text")
                .background(.blue)
        }
    }
}
```

在读取视图的框架时， `GeometryProxy` 提供的是 `frame(in:)` 方法，而不是简单的属性。因为 "frame" 的概念包括 X 坐标和 Y 坐标，而这两个坐标孤立地看没有任何意义。

SwiftUI 将这些选项称为坐标空间，其中两个特别的空间被称为 **global 空间**（测量相对于整个屏幕的视图框架）和 **local 空间**（测量相对于其父视图的视图框架）。还能通过将 `coordinateSpace()` 修饰符附加到视图来创建**自定义坐标空间**--该视图的子视图都能读取其相对于该坐标空间的框架。

一个例子如下：

```swift
 print("Global center: \(proxy.frame(in: .global).midX) x \(proxy.frame(in: .global).midY)")
```

## 用于给 ScrollView 添加特效

以前，我们用 `DragGesture` 将宽度和高度存储为 `@State` 属性，这样就可以根据拖动量调整其他属性。不过，通过 `GeometryReader` ，我们可以从视图的环境中动态抓取值，将其绝对或相对位置输入到各种修改器中。更妙的是，您可以根据需要嵌套几何图形读取器，这样一个读取器可以读取上一级视图的几何图形。

```swift
.rotation3DEffect(.degrees(proxy.frame(in: .global).minY / 5), axis: (x: 0, y: 1, z: 0))
```

#swiftui 