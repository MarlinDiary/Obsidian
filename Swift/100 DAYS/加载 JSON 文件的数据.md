1. 建立相应的数据[[结构 - Struct]]（符合 [[归档数据 - Codable]] 和 [[可识别协议 - Identifiable]]）

```swift
struct Astronaut: Codable, Identifiable {
    let id: String
    let name: String
    let description: String
}
```

2. 为 [[捆绑包 - Bundle]] 添加 [[扩展 - Extension]]（可配合[[泛型 - generics]]增加通用性）

```swift
extension Bundle {
    func decode(_ file: String) -> [String: Astronaut] {
        guard let url = self.url(forResource: file, withExtension: nil) else {
            fatalError("Failed to locate \(file) in bundle.")
        }

        guard let data = try? Data(contentsOf: url) else {
            fatalError("Failed to load \(file) from bundle.")
        }

        let decoder = JSONDecoder()

        guard let loaded = try? decoder.decode([String: Astronaut].self, from: data) else {
            fatalError("Failed to decode \(file) from bundle.")
        }

        return loaded
    }
}
```

3. 解码

```swift
let astronauts = Bundle.main.decode("astronauts.json")
```

#data #hard 