.tag() 修改器允许我们为每个[[拾取器 - Picker]]选项附加我们所选择的特定值。

```swift
Picker("Sort", selection: $sortOrder) {
    Text("Sort by Name")
        .tag([
            SortDescriptor(\User.name),
            SortDescriptor(\User.joinDate),
        ])

    Text("Sort by Join Date")
        .tag([
            SortDescriptor(\User.joinDate),
            SortDescriptor(\User.name)
        ])
}
```

#swiftui #easy 