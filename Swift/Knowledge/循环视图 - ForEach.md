ForEach 是一种[[结构 - Struct]]，它可以在 **数组** 和 **范围** 上循环，根据需要创建任意多个视图。

以下是循环 [[数组 - Array]] 的第一种方式：

```swift
VStack {
    ForEach(0..<agents.count) {
        Text(agents[$0])
    }
}
```

以下是循环数组的第二种方式（直接循环数组，但这需要多花点心思，因为 SwiftUI 想知道如何识别数组中的每个项）：

```swift
struct ContentView: View {
    let students = ["Harry", "Hermione", "Ron"]
    @State private var selectedStudent = "Harry"

    var body: some View {
        NavigationStack {
            Form {
                Picker("Select your student", selection: $selectedStudent) {
                    ForEach(students, id: \.self) {
                        Text($0)
                    }
                }
            }
        }
    }
}
```

`id: \.self` 部分非常重要。这样做是因为 SwiftUI 需要能够唯一识别屏幕上的每个视图，以便在发生变化时进行检测。

SwiftUI 最不愿意做的事情就是在每次进行微小改动时都丢弃整个布局并从头开始。相反，它希望尽可能减少工作量：保留现有的四个视图，只添加第五个视图。

#struct #loop #swiftui 