可以将一个[[可选项 - Optional]]与[[警报 - Alert]]或[[弹出窗口 - sheet]]绑定。关键是使用一个可选的 `Identifiable` 对象作为唤醒条件，闭包会将用于条件的非可选值返回，供你使用。

比如，有如下符合 `Identifiable` 协议的结构：

```swift
struct User: Identifiable {
    var id = "Taylor Swift"
}
```

有如下可选项：

```swift
@State private var selectedUser: User? = nil
```

在以下代码的帮助下，只要点击 "Tap Me"，就会出现一个显示 "Taylor Swift" 的工作表。一旦退出工作表，SwiftUI 就会将 `selectedUser` 设回 `nil` ：

```swift
Button("Tap Me") {
    selectedUser = User()
}
.sheet(item: $selectedUser) { user in
    Text(user.id)
}
```

alert 具有类似的功能，不过需要同时传递**布尔值**和**可选的 Identifiable 值**：

```swift
@State private var isShowingUser = false
```

```swift
.alert("Welcome", isPresented: $isShowingUser, presenting: selectedUser) { user in
    Button(user.id) { }
}
```

#optional 