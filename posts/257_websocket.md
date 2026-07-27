# websocket

WebSocket 是一种在单个 TCP 连接上进行全双工通信的协议。它提供了一种在 Web 应用程序中进行实时通信的方式，使得服务器和客户端之间可以实时地进行双向数据传输。

在 WebSocket 协议中，建立连接时需要通过 HTTP/HTTPS 进行握手，建立成功后就可以进行双向通信，而不需要像 HTTP 一样每次请求都需要重新建立连接。因此，WebSocket 在实现实时通信和推送等功能方面具有很大的优势。

在前端开发中，WebSocket 经常被用于实现实时聊天、在线游戏、实时数据传输等功能。

在 webpack-dev-server 中，WebSockets 也被用于实现 HMR Socket Server，实现了实时的模块更新和热重载功能。

