与工作表和警报一样，我们告诉 SwiftUI 何时触发效果，它就会为我们处理剩下的事情。

## 方法一：内置效果

比如让 counter 这一个变量作为触发器：

```swift
.sensoryFeedback(.increase, trigger: counter)
```

`.increase` 是内置触觉反馈之一，还有许多其他的可选，如`.success` 、 `.warning` 、 `.error` 、 `.start` 、 `.stop` 等。

## 方法二：更多控制

如果您想对触觉效果进行更多控制，有一种名为 `.impact()` 的替代。

它有两种变体，一种是指定对象的灵活性和效果的强度：

```swift
.sensoryFeedback(.impact(flexibility: .soft, intensity: 0.5), trigger: counter)
```

一种是您可以指定重量和强度：

```swift
.sensoryFeedback(.impact(weight: .heavy, intensity: 1), trigger: counter)
```

## 方法三：Core Haptics 框架

Core Haptics 可让我们结合轻敲、连续振动、参数曲线等多种方式，创建高度可定制的触觉效果。

1. 在 ContentView.swift 顶部附近添加这个新的 import：

```swift
import CoreHaptics
```

2. 创建一个 `CHHapticEngine` 的实例作为属性：

```swift
@State private var engine: CHHapticEngine?
```

3. 用方法启动 engine：

```swift
func prepareHaptics() {
    guard CHHapticEngine.capabilitiesForHardware().supportsHaptics else { return }

    do {
        engine = try CHHapticEngine()
        try engine?.start()
    } catch {
        print("There was an error creating the engine: \(error.localizedDescription)")
    }
}
```

4. 配置参数来控制触觉的强度（ `.hapticIntensity` ）和 "锐利 "度（ `.hapticSharpness` ），然后将这些参数置入具有相对时间偏移的触觉事件中：

```swift
func complexSuccess() {
    // make sure that the device supports haptics
    guard CHHapticEngine.capabilitiesForHardware().supportsHaptics else { return }
    var events = [CHHapticEvent]()

    // create one intense, sharp tap
    let intensity = CHHapticEventParameter(parameterID: .hapticIntensity, value: 1)
    let sharpness = CHHapticEventParameter(parameterID: .hapticSharpness, value: 1)
    let event = CHHapticEvent(eventType: .hapticTransient, parameters: [intensity, sharpness], relativeTime: 0)
    events.append(event)

    // convert those events into a pattern and play it immediately
    do {
        let pattern = try CHHapticPattern(events: events, parameters: [])
        let player = try engine?.makePlayer(with: pattern)
        try player?.start(atTime: 0)
    } catch {
        print("Failed to play pattern: \(error.localizedDescription).")
    }
}
```

5. 要试用我们的自定义触觉，请将 `ContentView` 的 `body` 属性修改为以下内容：

```swift
Button("Tap Me", action: complexSuccess)
    .onAppear(perform: prepareHaptics)
```

#swiftui 