# HMR Soket Server

HMR Socket Server 是 webpack HMR 的核心组件之一，它负责在开发模式下与浏览器端建立一个 WebSocket 长连接，以实现模块的[热更新]()。

在 webpack-dev-server 启动时，会创建一个 HMR Socket Server，它会监听一些事件（如编译完成、模块更新等）并发送相应的消息给浏览器端，以通知浏览器进行相应的处理。当 HMR Socket Server 接收到来自浏览器端的请求时，它会向浏览器端发送当前编译的模块的更新信息，包括更新的模块代码、新的依赖关系和 manifest 等信息。

HMR Socket Server 会生成两个文件：一个是 manifest 文件，另一个是 update chunk 文件。manifest 文件记录了所有模块的 ID 和 hash 值，以及模块之间的依赖关系，用于判断模块是否需要更新；update chunk 文件包含了所有需要更新的模块的代码，用于更新浏览器端的模块。

HMR Socket Server 通过 WebSocket 长连接与浏览器端通信，因此可以在模块发生变化时，立即将更新的模块代码发送到浏览器端，实现了实时的模块热更新。在浏览器端接收到更新后，会使用 HMR runtime 来解析和处理更新后的模块代码，以实现模块的热更新。
