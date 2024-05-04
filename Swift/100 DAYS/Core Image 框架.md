Core Image 是苹果处理图像的框架。经常用于锐化、模糊、晕染、像素化等。

1. 首先，我们要输入一些代码来生成基本图像。

```swift
struct ContentView: View {
    @State private var image: Image?

    var body: some View {
        VStack {
            image?
                .resizable()
                .scaledToFit()
        }
        .onAppear(perform: loadImage)
    }

    func loadImage() {
        image = Image(.example)
    }
}
```

之所以这么写代码，是因为要和 Core Image 配合。

Image 视图只是用于读取图像，我们无法将其内容写入磁盘，也无法对其进行其他转换。

如果我们要使用 Core Image，SwiftUI 的 `Image` 视图是一个很好的**终点**。也就是说，如果我们想**动态**创建图像、应用 Core Image 滤镜等，那么 SwiftUI 的 `Image` 就不能胜任这项工作。

2. 正确地使用图像类型。

苹果为我们提供了其他三种图像类型，如果我们想使用 Core Image，就必须使用这三种类型。

- `UIImage` ，来自 UIKit。这是一种极其强大的图像类型，能够处理各种图像类型，包括位图（如 PNG）、矢量图（如 SVG），甚至是形成动画的序列。 `UIImage` 是 UIKit 的标准图像类型，在这三种类型中，它最接近 SwiftUI 的 `Image` 类型。
- `CGImage` ，来自 Core Graphics。这是一种更简单的图像类型，实际上只是个二维像素数组。
- `CIImage` ，它来自核心图像。它存储了生成图像所需的所有信息，但实际上并不会将这些信息转化为像素，除非要求它这样做。Apple 将 `CIImage` 称为 "图像配方"，而非实际图像。

图像类型间有一定的互操作性。

- 可以从 `CGImage` 创建 `UIImage` ，并从 `UIImage` 创建 `CGImage`；
- 可以从 `UIImage` 和 `CGImage` 创建 `CIImage` ，也可以从 `CIImage` 创建 `CGImage`；
- 可以通过 `UIImage` 和 `CGImage` 创建 SwiftUI `Image`。

所以，我们应该更改 `loadImage()` 使其从示例图像中创建 `UIImage` ，然后将它转换成 `CIImage`（这正是 Core Image 想要使用的）：

```swift
func loadImage() {
    let inputImage = UIImage(resource: .example)
    let beginImage = CIImage(image: inputImage)

    // more code to come
}
```

3. 创建一个 Core Image context 和一个 Core Image filter。

- 上下文：负责将处理后的数据转换为我们可以使用的 `CGImage` 格式
- 过滤器：负责对图像数据进行实际转换，例如模糊、锐化、调整颜色等

这两种数据类型都来自 Core Image，因此需要添加两个导入：

```swift
import CoreImage
import CoreImage.CIFilterBuiltins
```

接下来，我们将创建 context 和 filter：

```swift
let context = CIContext()
let currentFilter = CIFilter.sepiaTone()
```

4. 可以自定义滤镜，改变它的工作方式。

`inputImage` 是我们要改变的图像， `intensity` 是应用效果的强度：

```swift
currentFilter.inputImage = beginImage
currentFilter.intensity = 1
```

不过，相比于用 `inputImage` 传入图像，更安全的方法是 setValue：

```swift
let beginImage = CIImage(image: inputImage)
currentFilter.setValue(beginImage, forKey: kCIInputImageKey)
applyProcessing()
```

5. 将过滤器的输出转换为 SwiftUI `Image` 并显示在视图中。

在这里，我们需要同时使用所有四种图像类型，最简单的方法是：CIImage → CGImage → UIImage → Image：

```swift
// get a CIImage from our filter or exit if that fails
guard let outputImage = currentFilter.outputImage else { return }

// attempt to get a CGImage from our CIImage
guard let cgImage = context.createCGImage(outputImage, from: outputImage.extent) else { return }

// convert that to a UIImage
let uiImage = UIImage(cgImage: cgImage)

// and convert that to a SwiftUI image
image = Image(uiImage: uiImage)
```

6. 第四步是现代 API 的滤镜自定义步骤，但较早的 API 可以帮助我们询问当前 filter 支持的值，然后发送给该 filter。

```swift
let currentFilter = CIFilter.twirlDistortion()
currentFilter.inputImage = beginImage

let amount = 1.0

let inputKeys = currentFilter.inputKeys

if inputKeys.contains(kCIInputIntensityKey) {
    currentFilter.setValue(amount, forKey: kCIInputIntensityKey) }
if inputKeys.contains(kCIInputRadiusKey) { currentFilter.setValue(amount * 200, forKey: kCIInputRadiusKey) }
if inputKeys.contains(kCIInputScaleKey) { currentFilter.setValue(amount * 10, forKey: kCIInputScaleKey) }
```

有了这些，哪怕 filter 换了，代码也将继续工作。每个调整值只有在 filter 支持的情况下才会被发送进来。

这种为键设置值的工作方式和 [[用户偏好数据 - UserDefaults]] 很像。

#framework 