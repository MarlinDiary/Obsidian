如果必须使两个视图对齐，而它们又位于用户界面的完全不同部分，那么 SwiftUI 自带的[[对齐 - Alignment|对齐]]选项便无法很好地发挥作用。

为了解决这个问题，SwiftUI 允许我们创建自定义对齐向导，并在整个用户界面的视图中使用。

这样一个自定义对齐向导应该是 `VerticalAlignment` 或 `HorizontalAlignment` 的 [[扩展 - Extension]]，并且是符合 `AlignmentID` [[协议 - Protocol]] 的自定义类型。

"自定义类型" 很可能会让人想到结构体，但将其作为 [[枚举 - Enum]] 来实现也是个不错的主意。

`AlignmentID` 协议只有一个要求，即符合该协议的类型必须有一个静态 `defaultValue(in:)` 方法，该方法接受一个 `ViewDimensions` ，并返回一个 `CGFloat` ，若视图没有 `alignmentGuide()` 修改器，则该方法将指定视图的对齐方式。

代码如下所示：

```swift
extension VerticalAlignment {
    struct MidAccountAndName: AlignmentID {
        static func defaultValue(in context: ViewDimensions) -> CGFloat {
            context[.top]
        }
    }

    static let midAccountAndName = VerticalAlignment(MidAccountAndName.self)
}

// 该静态常量是为了更方便地使用自定义对齐
```

不过，使用枚举比使用结构体更可取，原因如下：`MidAccountAndName` 结构体的存在意味着我们可以（如果我们愿意）创建该结构体的实例，尽管这样做没有任何意义，因为它没有任何功能。如果将 `struct MidAccountAndName` 替换为 `enum MidAccountAndName` ，那么就无法再创建一个实例了--这就更清楚地表明，这个东西的存在只是为了容纳某些功能。

无论选择的是枚举还是结构体，它的用法都是一样的：将其设置为 Stack 的对齐方式，然后使用 `alignmentGuide()` 在任何需要对齐的视图上激活它。这只是一个 Guide：它可以帮助你将视图沿单线对齐，但并不说明视图应如何对齐。这就意味着仍然需要为 `alignmentGuide()` 提供 [[闭包 - Closure]]，以便按照您的要求将视图沿着该 Guide 定位。

示例代码如下所示：

```swift
HStack(alignment: .midAccountAndName) {
    VStack {
        Text("@twostraws")
            .alignmentGuide(.midAccountAndName) { d in d[VerticalAlignment.center] }
        Image(.paulHudson)
            .resizable()
            .frame(width: 64, height: 64)
    }

    VStack {
        Text("Full name:")
        Text("PAUL HUDSON")
            .alignmentGuide(.midAccountAndName) { d in d[VerticalAlignment.center] }
            .font(.largeTitle)
    }
}
```

#swiftui #hard 