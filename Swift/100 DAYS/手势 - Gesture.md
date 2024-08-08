## 简单手势

| 修改器                   | 作用         | 参数              | 作用        |
| --------------------- | ---------- | --------------- | --------- |
| `.onTapGesture`       | 当用户轻点视图时触发 | count           | 双击、三击     |
| `.onLongPressGesture` | 当用户长按视图时触发 | minimumDuration | 长按的最短持续时间 |

## onPressingChanged 闭包

在**长按手势**的状态发生变化时触发。该闭包的输入为一个布尔参数，其工作原理如下：

1. 一旦按下：布尔参数将被设置为 true
2. 在手势被识别前松开：布尔参数将被设置为 false
3. 整个识别过程中一直按住不放：最终布尔参数将被设置为 false

下面是一个可能的代码：

```swift
Text("Hello, World!")
    .onLongPressGesture(minimumDuration: 1) {
        print("Long pressed!")
    } onPressingChanged: { inProgress in
        print("In progress: \(inProgress)!")
    }
```

## 高级手势

对于更高级的手势，应使用 `gesture()` 修饰符和其中一种手势[[结构 - Struct|结构]]： `DragGesture` , `LongPressGesture` , `MagnifyGesture` , `RotateGesture` 和 `TapGesture` 。

这些手势又都有特殊的修饰符，通常为 `onEnded()` ，也经常为 `onChanged()` ，可以凭借这些修饰符在手势进行中（ `onChanged()` ）或完成时（ `onEnded()` ）采取行动。

1. **Magnify Gesture**：

```swift
struct ContentView: View {
    @State private var currentAmount = 0.0
    @State private var finalAmount = 1.0

    var body: some View {
        Text("Hello, World!")
            .scaleEffect(finalAmount + currentAmount)
            .gesture(
                MagnifyGesture()
                    .onChanged { value in
                        currentAmount = value.magnification - 1
                    }
                    .onEnded { value in
                        finalAmount += currentAmount 
                        currentAmount = 0
                    }
            )
    }
}
```

2. **Rotate Gesture**：

```swift
struct ContentView: View {
    @State private var currentAmount = Angle.zero
    @State private var finalAmount = Angle.zero

    var body: some View {
        Text("Hello, World!")
            .rotationEffect(currentAmount + finalAmount)
            .gesture(
                RotateGesture()
                    .onChanged { value in
                        currentAmount = value.rotation
                    }
                    .onEnded { value in
                        finalAmount += currentAmount
                        currentAmount = .zero
                    }
            )
    }
}
```

## 多手势叠加

1. 在以下父子视图同时包含手势的情况下，SwiftUI 将始终优先使用子手势：

```swift
struct ContentView: View {
    var body: some View {
        VStack {
            Text("Hello, World!")
                .onTapGesture {
                    print("Text tapped")
                }
        }
        .onTapGesture {
            print("VStack tapped")
        }
    }
}

// 将会显示 "Text tapped"
```

2. 不过，可以使用 `highPriorityGesture()` 修饰符强制父手势触发：

```swift
struct ContentView: View {
    var body: some View {
        VStack {
            Text("Hello, World!")
                .onTapGesture {
                    print("Text tapped")
                }
        }
        .highPriorityGesture(
            TapGesture()
                .onEnded {
                    print("VStack tapped")
                }
        )
    }
}
```

3. 也可以使用 `simultaneousGesture()` 修饰符告诉 SwiftUI，父手势和子手势同时触发：

```swift
struct ContentView: View {
    var body: some View {
        VStack {
            Text("Hello, World!")
                .onTapGesture {
                    print("Text tapped")
                }
        }
        .simultaneousGesture(
            TapGesture()
                .onEnded {
                    print("VStack tapped")
                }
        )
    }
}
```

## 手势序列

手势序列指的是一个手势只有在另一个手势成功时才会激活。

下面的示例展示了手势排序功能，您可以拖动圆圈，但前提是先长按圆圈：

```swift
struct ContentView: View {
    // how far the circle has been dragged
    @State private var offset = CGSize.zero

    // whether it is currently being dragged or not
    @State private var isDragging = false

    var body: some View {
        // a drag gesture that updates offset and isDragging as it moves around
        let dragGesture = DragGesture()
            .onChanged { value in offset = value.translation }
            .onEnded { _ in
                withAnimation {
                    offset = .zero
                    isDragging = false
                }
            }

        // a long press gesture that enables isDragging
        let pressGesture = LongPressGesture()
            .onEnded { value in
                withAnimation {
                    isDragging = true
                }
            }

        // a combined gesture that forces the user to long press then drag
        let combined = pressGesture.sequenced(before: dragGesture)

        // a 64x64 circle that scales up when it's dragged, sets its offset to whatever we had back from the drag gesture, and uses our combined gesture
        Circle()
            .fill(.red)
            .frame(width: 64, height: 64)
            .scaleEffect(isDragging ? 1.5 : 1)
            .offset(offset)
            .gesture(combined)
    }
}
```

#swiftui #hard 