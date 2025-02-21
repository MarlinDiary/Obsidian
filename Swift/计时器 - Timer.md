iOS 内置的 `Timer` 类可让我们定期运行代码。

## 创建 Timer Publisher 

```swift
let timer = Timer.publish(every: 1, on: .main, in: .common).autoconnect()
```

它同时做了几件事：

1. 要求 Timer 每 1 秒计时一次
2. 要求 Timer 在主线程（main thread）运行
3. 要求 Timer 在常用（common）的 run loop 中运行
4. 要求 Timer 立即连接（auto connect）并开始计时
5. 整个内容将被赋值给常量 timer

## 监控通告

可以使用名为 `onReceive()` 的修改器在 SwiftUI 中监控 timer 所发出的通告。

第一个参数是 publisher，第二个是 function，它会确保在发布者发送变更通告时调用该函数：

```swift
Text("Hello, World!")
    .onReceive(timer) { time in
        print("The time is now \(time)")
    }
```

## 停止 Timer

上文的 timer 是个  auto-connected publisher，因此需要转到它的 upstream publisher，找到定时器本身。在那里，我们可以连接到 timer publisher，并要求它自我取消。

```swift
Text("Hello, World!")
            .onReceive(timer) { time in
                if counter == 5 {
                    timer.upstream.connect().cancel()
                } else {
                    print("The time is now \(time)")
                }

                counter += 1
            }
```

## 增加 Timer 的容差

如果你不介意定时器有一点浮动，你可以指定一些容差（tolerance）。

这意味着系统可以执行**定时器聚合**：系统可以将你的定时器**推后**一点，使其与一个或多个其他定时器同时启动。这种聚合不仅可以让 CPU 保持更多空闲，还可以节省电池电量。

这将为我们的计时器增加半秒的容差：

```swift
let timer = Timer.publish(every: 1, tolerance: 0.5, on: .main, in: .common).autoconnect()
```

#swiftui #class #hard 