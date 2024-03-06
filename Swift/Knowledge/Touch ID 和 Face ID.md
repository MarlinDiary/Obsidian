1. 写代码前，需在项目选项中添加新密钥，向用户解释为什么要访问 Face ID。由于只有苹果知道的原因，我们在**代码**中传递 **Touch ID** 申请理由，在**项目选项**中传递 **Face ID** 申请理由。

转到 Info tab → 右键单击一个 existing key → 选择 Add Row → 滚动到 Privacy - Face ID Usage Description → 给它赋值为 “We need to unlock your data.”

2. 在文件顶部附近添加此导入：

```swift
import LocalAuthentication
```

3. Swift 开发人员用 `Error` 协议表示运行时出现的错误，而 Objective-C 用名为 `NSError` 的特殊类。我们需要将该类传递到函数中，并在函数内部对其进行更改，对于这种 in-out 传递形式，我们需要使用 `&` 来特别标记这种行为。.

可以通过四步来编写一个 `authenticate()` 方法：

- 创建 `LAContext` 的实例，这样就可以**查询生物识别状态**和执行**授权检查**
- 询问该 context **是否**能够执行生物识别身份验证
- 如果能够执行，我们就会**启动**身份验证请求，并在身份验证完成后传递一个**闭包**
- 当用户通过或未通过身份验证时，我们的完成**闭包**将被调用

```swift
func authenticate() {
    let context = LAContext()
    var error: NSError?

    // check whether biometric authentication is possible
    if context.canEvaluatePolicy(.deviceOwnerAuthenticationWithBiometrics, error: &error) {
        // it's possible, so go ahead and use it
        let reason = "We need to unlock your data."

        context.evaluatePolicy(.deviceOwnerAuthenticationWithBiometrics, localizedReason: reason) { success, authenticationError in
            // authentication has now completed
            if success {
                // authenticated successfully
            } else {
                // there was a problem
            }
        }
    } else {
        // no biometrics
    }
}
```

4. 需添加状态，以便身份验证成功时进行调整，还要添加 `onAppear()` 修饰符来触发身份验证。

- 首先将此属性添加到 `ContentView` 中：

```swift
@State private var isUnlocked = false
```

- 用以下注释替换 `// authenticated successfully` 注释：

```swift
isUnlocked = true
```

- 最后，我们可以开始身份验证过程：

```swift
.onAppear(perform: authenticate)
```

5. 使用 Face ID：Simulator → Features → Face ID → Enrolled

#framework 