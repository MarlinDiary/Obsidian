异步函数是指能够暂时休眠的函数，这样它就可以等待其他工作完成后再继续运行。比如，在网络代码运行时进入休眠状态，这样应用程序的其他部分就不会冻结数秒。

1. 向结构中添加方法。

```swift
func loadData() async {

}
```

2. 我们希望在显示 `List` 时立即运行该函数，但这里不能使用 [[启动运行 - onAppear]] ，对于异步函数我们要用 task 修饰符。

```swift
.task {
    await loadData()
}
```

Swift 要求我们做的就是用第二个关键字 `await` 标记这些函数，这样就明确承认可能会发生休眠。

将 `await` 视为 `try` - 我们是在说我们知道可能会发生休眠，就像 `try` 表示我们承认可能会抛出错误一样。

3. 在 `loadData()` 中，我们还需要完成三个步骤。

a. 创建我们要读取的 URL

```swift
guard let url = URL(string: "https://itunes.apple.com/search?term=taylor+swift&entity=song") else {
    print("Invalid URL")
    return
}
```

b. 获取该 URL 的数据

```swift
do {
    let (data, _) = try await URLSession.shared.data(from: url)

    // more code to come
} catch {
    print("Invalid data")
}
```

- 我们的工作由 `data(from:)` 方法完成，该方法接收一个 URL 并返回该 URL 上的 `Data` 对象。
- `data(from:)` 的返回值是一个元组，包含 URL 中的数据和一些描述请求过程的元数据。我们不使用元数据，但我们需要 URL 的 data，因此使用了下划线--我们为数据创建了一个新的本地常量，并将元数据丢弃。
- 同时使用 `try` 和 `await` 时，必须写 `try await`，不许用 `await try` ，这没有特别的原因。

c. 将数据结果解码为现有的结构（[[加载 JSON 文件的数据]]）

```swift
if let decodedResponse = try? JSONDecoder().decode(Response.self, from: data) {
    results = decodedResponse.results
}
```

#data #hard 