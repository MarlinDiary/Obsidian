Result 允许我们在单个数据中封装**成功值**或**某种错误类型**。

现在有一个从服务器上下载数组的[[异步函数 - Asynchronous Function|方法]]：

```swift
struct ContentView: View {
    @State private var output = ""

    var body: some View {
        Text(output)
            .task {
                await fetchReadings()
            }
    }

    func fetchReadings() async {
        do {
            let url = URL(string: "https://hws.dev/readings.json")!
            let (data, _) = try await URLSession.shared.data(from: url)
            let readings = try JSONDecoder().decode([Double].self, from: data)
            output = "Found \(readings.count) readings"
        } catch {
            print("Download error")
        }
    }
}
```

借助 [[任务 - Task]]，可以将上述代码重写成这样：

```swift
func fetchReadings() async {
    let fetchTask = Task {
        let url = URL(string: "https://hws.dev/readings.json")!
        let (data, _) = try await URLSession.shared.data(from: url)
        let readings = try JSONDecoder().decode([Double].self, from: data)
        return "Found \(readings.count) readings"
    }
}
```

如果网络获取失败或数据解码失败， `Task` 可能会出错，这就是 `Result` 的作用所在：Task 的结果可能是一个字符串，也可能是一个错误。唯一的办法就是查看其中的内容--与[[可选项 - Optional|可选项]]相似。

可以这样读取其 `result` 属性：

```swift
let result = await fetchTask.result
```

可以直接从 `Result` 中读取成功值，但需要适当处理错误：

```swift
do {
    output = try result.get()
} catch {
    output = "Error: \(error.localizedDescription)"
}
```

也可以在 `Result` 上 [[条件 - Switch]]：

```swift
switch result {
    case .success(let str):
        output = str
    case .failure(let error):
        output = "Error: \(error.localizedDescription)"
}

//每种 case 都有其内部值，要用特殊的 let 来匹配
```

总而言之，`Result` 的优势在于它可以将某些工作的成功或失败信息存储在一个值中，在需要的地方进行传递，只有在准备就绪时才读取错误信息。

#type 