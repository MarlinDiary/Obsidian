当特定值发生变化，onChange [[修改器 - Modifier]]会告诉 SwiftUI 运行我们选择的[[闭包 - Closure]]。

SwiftUI 会自动将新旧值传递给闭包，因此我们可以这样使用它：

```swift
struct ContentView: View {
    @State private var blurAmount = 0.0

    var body: some View {
        VStack {
            Text("Hello, World!")
                .blur(radius: blurAmount)

            Slider(value: $blurAmount, in: 0...20)
                .onChange(of: blurAmount) { oldValue, newValue in
                    print("New value is \(newValue)")
                }
        }
    }
}
```

#swiftui #easy 