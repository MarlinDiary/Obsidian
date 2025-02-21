如果有重要事情发生，通知用户的常用方法是使用警报--弹出窗口，其中包含标题、信息和一个或两个按钮。

**视图是程序状态的函数**，警报也不例外。因此，与其说 "显示警报"，不如创建警报并设置显示条件。

我们要创建一些 [[属性包装器#@State]] 来跟踪警报是否显示，就像这样：

```swift
@State private var showingAlert = false
```

然后，我们将警报附加到用户界面的某处，告诉它使用该 State 来决定是否显示警报。SwiftUI 将监视 `showingAlert` 状态，一旦该状态变为 true，就会显示警报。

```swift
struct ContentView: View {
    @State private var showingAlert = false

    var body: some View {
        Button("Show Alert") {
            showingAlert = true
        }
        .alert("Important message", isPresented: $showingAlert) {
            Button("OK") { }
        }
    }
}
```

这样就将警报附加到了按钮上，但老实说，**在哪里使用 `alert()` 修饰符并不重要，我们所做的只是说存在一个警报，并在 `showingAlert` 为 true 时显示出来。**

警报中的任何[[按钮 - Button]]都会自动解除警报，而闭包的作用就是让我们添加解除警报之外的任何额外功能。

最后，您可以用第二个尾随[[闭包 - Closure]]的方式，在标题旁边添加信息文本，就像这样：

```swift
Button("Show Alert") {
    showingAlert = true
}
.alert("Important message", isPresented: $showingAlert) {
    Button("OK", role: .cancel) { }
} message: {
    Text("Please read this.")
}
```

提示：如果你不在代码中包含任何[[按钮 - Button]]，你就会自动获得一个简单的 "OK "按钮来解除警报：

```swift
.alert(errorTitle, isPresented: $showingError) { } message: {
    Text(errorMessage)
}
```

#swiftui #closure #easy 