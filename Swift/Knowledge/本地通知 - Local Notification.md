iOS 有一个名为 UserNotifications 的框架，让我们为用户创建可显示在锁屏上的通知。

1. 在 ContentView.swift 顶部附近添加一个额外的导入：

```swift
import UserNotifications
```

2. 一个按钮用于征求用户许可，一个按钮用于安排通知：

```swift
VStack {
    Button("Request Permission") {
        // first
    }

    Button("Schedule Notification") {
        // second
    }
}
```

3. 当告诉 iOS 我们想要哪种通知时，它会向用户显示一个提示，这样用户就能对我们的程序能做什么有最终决定权。当用户做出选择后，闭包将被调用，并告诉我们请求是否成功：

```swift
UNUserNotificationCenter.current().requestAuthorization(options: [.alert, .badge, .sound]) { success, error in
    if success {
        print("All set!")
    } else if let error {
        print(error.localizedDescription)
    }
}
```

4. 如果用户同意，我们就可以开始安排通知：

```swift
let content = UNMutableNotificationContent()
content.title = "Feed the cat"
content.subtitle = "It looks hungry"
content.sound = UNNotificationSound.default

// show this notification five seconds from now
let trigger = UNTimeIntervalNotificationTrigger(timeInterval: 5, repeats: false)

// choose a random identifier
let request = UNNotificationRequest(identifier: UUID().uuidString, content: content, trigger: trigger)

// add our notification request
UNUserNotificationCenter.current().add(request)
```

- **Content** 是应该显示的内容，可以是 title, subtitle, sound, image 等
- **Trigger** 决定何时显示通知，可以是几秒后、未来的某个日期和时间，也可以是某个位置
- **Request** 不仅结合了 content 和 trigger，还添加了一个唯一 identifier，以便以后编辑或删除特定警报，如果不想编辑或删除内容，可使用 `UUID().uuidString` 获取随机 identifier

#framework 