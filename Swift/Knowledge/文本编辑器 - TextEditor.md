[[输入 - TextField]] 视图非常适合用户输入短小的文本，如果要输入较长的文本，可能需要改用 `TextEditor` 视图。它的额外优势是允许输入多行文本，更适合为用户提供大量的工作空间。

```swift
TextEditor(text: $notes)
```

当然，还有第三种选择：当我们创建 `TextField` 时，我们可以选择提供一个可以沿其增长的轴。

```swift
struct ContentView: View {
    @AppStorage("notes") private var notes = ""

    var body: some View {
        NavigationStack {
            TextField("Enter your text", text: $notes, axis: .vertical)
                .textFieldStyle(.roundedBorder)
                .navigationTitle("Notes")
                .padding()
        }
    }
}
```

#swiftui 