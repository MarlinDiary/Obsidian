该类型与 URL 相似，但它为我们提供了添加额外信息（如请求类型、用户数据等）的选项。

我们需要以非常特殊的方式附加数据，以便服务器能正确处理，这意味着除了数据本身之外，我们还需要提供两个额外的数据：

1. 请求的 HTTP 方法决定了数据的发送方式。HTTP 方法有多种，但在实际应用中，只有 GET（"我想读取数据"）和 POST（"我想写入数据"）使用较多。
2. 请求的内容类型决定了正在发送的数据种类，这影响了服务器处理我们数据的方式。这是通过所谓的 MIME 类型来指定的，MIME 类型最初是为了在电子邮件中发送附件而制定的，它有几千种高度具体的选项。

#type #data #hard 