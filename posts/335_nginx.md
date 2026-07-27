# Nginx

Nginx是一个高性能的 **HTTP 服务器** 和 **反向代理服务器**，同时也可以作为 **邮件代理服务器** 和通用的 **TCP/UDP 代理服务器**。它由俄罗斯程序员伊戈尔·赛索耶夫开发，于2004年首次公开发布。Nginx 以其高并发、低内存占用、高稳定性以及丰富的功能集而闻名，目前被全球大量网站使用（包括Netflix、WordPress、GitHub等）。

## 核心特点

- **事件驱动架构**：不同于传统的每个连接一个进程/线程的模式，Nginx 使用异步、非阻塞的事件驱动模型（如 epoll、kqueue），能够高效处理成千上万的并发连接。
- **低资源消耗**：在相同负载下，Nginx 的内存和 CPU 占用通常远低于 Apache 等传统服务器。
- **高扩展性**：支持模块化设计，核心非常精简，大量功能通过静态或动态模块实现（如 Gzip、SSL、Lua 脚本等）。
- **高可靠性**：成熟稳定的代码库，许多大型网站长期运行数月甚至数年无需重启。

## 主要功能

### 1. 静态文件服务

Nginx 特别擅长快速、高效地托管静态资源（HTML、CSS、JS、图片等），通过 `sendfile` 等优化直接将文件从磁盘发送到网络。

### 2. 反向代理与负载均衡

- **反向代理**：将客户端请求转发到后端服务器（如应用服务器、其他 Web 服务器），并将响应返回给客户端。可以隐藏后端细节、增加安全性和灵活性。
- **负载均衡**：支持多种均衡算法，如轮询、最少连接、IP哈希等，将流量分发到多个后端节点。
- **健康检查**：自动标记故障的后端服务器，避免向其转发请求。

### 3. HTTP 缓存

可以作为缓存服务器，缓存后端响应的内容，减轻后端压力，加速用户访问。

### 4. SSL/TLS 支持

提供完整的 HTTPS 支持，包括 SNI、OCSP stapling、HSTS 等。性能优秀的 SSL 会话复用和硬件加速。

### 5. 访问控制与安全

- 基于 IP 的访问限制
- 身份验证（HTTP Basic、Digest 等）
- 限速（限制请求频率、并发连接、带宽）
- 防御简单 DDoS 攻击（`limit_req`、`limit_conn`）

### 6. URL 重写与重定向

强大的 `rewrite` 模块支持正则表达式，实现灵活的 URL 路由、伪静态规则。

### 7. 其他协议代理

- **FastCGI**（与 PHP-FPM 配合处理 PHP 动态内容）
- **uWSGI**（与 Python 应用）
- **SCGI**
- **gRPC**
- **WebSocket**（支持协议升级）
- TCP/UDP 流代理（用于数据库、Redis、DNS 等）

## 工作原理简述

Nginx 采用 **master-worker** 多进程模型：

- 一个 **master 进程**，负责读取配置、绑定端口、管理工作进程（启动、停止、热加载配置）。
- 多个 **worker 进程**，真正处理客户端请求。每个 worker 独立运行，通过共享监听套接字接受新连接，并使用事件循环（epoll 等）非阻塞地处理所有连接的读/写事件。

这种设计使得：

- 即使一个 worker 崩溃，master 会立即启动新的 worker，服务不中断。
- 多核 CPU 利用率高（每个 worker 可绑定到特定 CPU 核心）。
- 连接均匀分布，无锁竞争。

## 常见使用场景

1. **静态资源服务器**：托管前端打包后的文件、图片、下载站。
2. **反向代理网关**：统一入口，将请求分发给后端微服务或传统应用服务器（Tomcat、Node.js、Gunicorn 等）。
3. **负载均衡器**：分发流量到多个后端实例，提升可用性和吞吐量。
4. **API 网关**：结合 Lua（OpenResty）实现鉴权、路由、限流等高级逻辑。
5. **缓存服务器**：缓存动态响应，作为 CDN 边缘节点或代理缓存。
6. **Web 加速**：与 Apache 组合使用，Nginx 在前端处理静态、代理动态，减轻 Apache 压力。
7. **Kubernetes Ingress Controller**：作为 Ingress 的实现之一，管理集群外部访问。

## Nginx vs Apache

| 特性       | Nginx                        | Apache                                                     |
| :--------- | :--------------------------- | :--------------------------------------------------------- |
| 架构       | 事件驱动，异步非阻塞         | 进程/线程驱动，同步阻塞（也有事件模型，但不如 Nginx 纯粹） |
| 并发处理   | 非常高，适合高并发           | 中等，每个连接消耗更多资源                                 |
| 静态文件   | 极快                         | 一般                                                       |
| 动态内容   | 通过代理至后端解释器         | 通过模块内嵌解释器（如 mod_php）                           |
| 配置灵活性 | 简洁，作用域规则清晰         | 非常灵活，`.htaccess` 支持目录级配置                       |
| 模块支持   | 核心模块固定，部分模块需编译 | 动态加载模块非常方便                                       |
| 内存占用   | 低                           | 较高（尤其是 prefork 模式）                                |

## 基本配置示例

```nginx
# 全局配置
user www-data;
worker_processes auto;
pid /run/nginx.pid;

events {
    worker_connections 1024;   # 每个 worker 最大连接数
    use epoll;
}

http {
    # 基础设置
    include mime.types;
    default_type application/octet-stream;
    sendfile on;
    keepalive_timeout 65;

    # 日志格式
    log_format main '$remote_addr - $remote_user [$time_local] "$request" '
                    '$status $body_bytes_sent "$http_referer" '
                    '"$http_user_agent"';
    access_log /var/log/nginx/access.log main;

    # 静态网站
    server {
        listen 80;
        server_name example.com;
        root /var/www/html;
        index index.html;

        location / {
            try_files $uri $uri/ =404;
        }
    }

    # 反向代理 + 负载均衡
    upstream backend {
        # 负载均衡算法：默认轮询，可加 ip_hash; 
        server 192.168.1.10:8080 weight=3;
        server 192.168.1.11:8080;
        server 192.168.1.12:8080 backup;
    }

    server {
        listen 80;
        server_name api.example.com;

        location / {
            proxy_pass http://backend;
            proxy_set_header Host $host;
            proxy_set_header X-Real-IP $remote_addr;
        }
    }
}
```



## 常用的衍生版本

- **OpenResty**：集成 Lua 脚本支持，可编写复杂逻辑，广泛用于 API 网关。
- **Tengine**：淘宝开源的 Nginx 增强版，增加了很多模块和特性。
- **Nginx Plus**：官方商业版，提供更丰富的负载均衡、监控、配置API等企业级功能。

## 总结

Nginx 已经成为现代互联网基础设施中不可或缺的一部分。它既能胜任边缘入口的流量管理，也能在后端高效提供静态内容。如果你正在构建一个需要处理高并发、低延迟或反向代理场景的系统，Nginx 几乎是默认的首选方案。





------

## 1. 全局配置（main 上下文）

```nginx
user www-data;
worker_processes auto;
pid /run/nginx.pid;
```

- **user www-data;**
  指定 Nginx worker 进程运行的操作系统用户和组。这里设置为 `www-data`（Debian/Ubuntu 下的常见 Web 用户）。
  **作用**：降低权限，提高安全性。如果 Nginx 被攻破，攻击者只会获得 `www-data` 的权限，而非 root。
- **worker_processes auto;**
  设置 worker 进程的数量。`auto` 表示 Nginx 会自动检测 CPU 核心数，并启动同样数量的 worker 进程。
  **作用**：充分利用多核 CPU 的并行处理能力。通常设置为 `auto` 或具体的核心数（如 `4`）。
- **pid /run/nginx.pid;**
  指定 Nginx 主进程（master）的 PID 文件存放位置。该文件记录主进程的进程号，方便系统工具（如 `nginx -s reload`）向主进程发送信号。

------

## 2. events 块

```nginx
events {
    worker_connections 1024;   # 每个 worker 最大连接数
    use epoll;
}
```

- **worker_connections 1024;**
  每个 worker 进程可以同时打开的最大连接数。
  **计算公式**：最大并发连接数 ≈ `worker_processes × worker_connections`。
  实际值还需考虑系统限制（如 `ulimit -n`）。1024 是保守值，高并发场景可设为 65535 或更高。
- **use epoll;**
  指定事件处理模型。`epoll` 是 Linux 下高效的事件通知机制（2.6+ 内核），适合高并发。
  Nginx 会根据操作系统自动选择最优模型（如 Linux 用 epoll，FreeBSD 用 kqueue），但显式指定可以避免自动检测的微小开销。

------

## 3. http 块

http 块是配置 HTTP 服务的主要地方，其中可以包含多个 `server` 虚拟主机。

### 3.1 基础设置

```nginx
include mime.types;
default_type application/octet-stream;
sendfile on;
keepalive_timeout 65;
```

- **include mime.types;**
  引入一个定义了 MIME 类型映射的文件（通常位于 `/etc/nginx/mime.types`）。该文件将文件扩展名（如 `.html`）映射到对应的 Content-Type（如 `text/html`）。
  **作用**：让浏览器正确处理不同类型的文件（图片、CSS、JS 等）。
- **default_type application/octet-stream;**
  当无法根据扩展名确定 MIME 类型时，使用的默认类型。`application/octet-stream` 会触发浏览器下载该文件（而不是尝试显示）。
  可以改为 `text/plain` 等，但一般保留默认。
- **sendfile on;**
  启用 Linux 的 `sendfile` 系统调用，让数据在磁盘和网络套接字之间直接传输，无需经过用户态缓冲区，大幅提升静态文件发送性能。
  **注意**：对于非静态内容（如反向代理）或某些特殊场景，可能需要关闭，但绝大多数情况应开启。
- **keepalive_timeout 65;**
  设置 HTTP 持久连接（Keep-Alive）的超时时间（秒）。超过 65 秒无新请求，服务器会关闭连接。
  **作用**：减少 TCP 握手开销，提高性能。值不宜过大（占用资源），也不宜过小（频繁建连）。65 秒是常用值。

### 3.2 日志设置

```nginx
log_format main '$remote_addr - $remote_user [$time_local] "$request" '
                '$status $body_bytes_sent "$http_referer" '
                '"$http_user_agent"';
access_log /var/log/nginx/access.log main;
```

- **log_format main ...**
  定义名为 `main` 的日志格式，使用 Nginx 内置变量：
  - `$remote_addr`：客户端 IP 地址。
  - `$remote_user`：HTTP 基本认证用户名（未认证则为 `-`）。
  - `$time_local`：服务器本地时间。
  - `$request`：请求行（如 `GET /index.html HTTP/1.1`）。
  - `$status`：响应状态码（如 200、404）。
  - `$body_bytes_sent`：响应体大小（不含响应头）。
  - `$http_referer`：Referer 请求头（来源页面）。
  - `$http_user_agent`：客户端 User-Agent。
    这是经典的 **combined** 格式变体。
- **access_log /var/log/nginx/access.log main;**
  将所有 HTTP 请求的访问日志记录到 `/var/log/nginx/access.log` 文件中，并使用上面定义的 `main` 格式。
  可以针对不同的 `server` 或 `location` 覆盖设置独立的日志文件。

### 3.3 第一个 server 块：静态网站

```nginx
server {
    listen 80;
    server_name example.com;
    root /var/www/html;
    index index.html;

    location / {
        try_files $uri $uri/ =404;
    }
}
```

- **listen 80;**
  监听 IPv4 的 80 端口（HTTP 默认端口）。也可以写作 `listen 80 default_server;` 指定默认服务器。
- **server_name example.com;**
  虚拟主机名，用于匹配请求的 `Host` 头。当客户端访问 `example.com`（且端口 80）时，此 `server` 块被选中。
  可以写多个域名，如 `server_name example.com www.example.com;`。
- **root /var/www/html;**
  定义网站的文档根目录。请求的 URI 会映射到该目录下的文件。例如 `GET /images/logo.png` → `/var/www/html/images/logo.png`。
- **index index.html;**
  定义目录索引文件。当请求以 `/` 结尾（例如 `/about/`）时，Nginx 会尝试返回 `/var/www/html/about/index.html`。
- **location / { ... }**
  匹配所有 URI 的位置块（`/` 匹配所有路径）。
  **try_files $uri $uri/ =404;**
  按顺序尝试处理请求：
  1. `$uri`：首先尝试以请求 URI 作为文件路径（如 `/var/www/html/foo.html`）。
  2. `$uri/`：如果没找到文件，尝试将该 URI 作为目录，并在目录下查找索引文件（`index.html`）。
  3. `=404`：如果前两步都失败，直接返回 HTTP 404 状态码。
     这是处理静态文件最经典、安全的方式（不会将请求转发到后端或列出目录内容）。

### 3.4 upstream 块：定义后端服务器组

```nginx
upstream backend {
    # 负载均衡算法：默认轮询，可加 ip_hash; 
    server 192.168.1.10:8080 weight=3;
    server 192.168.1.11:8080;
    server 192.168.1.12:8080 backup;
}
```

- **upstream backend { ... }**
  定义一个名为 `backend` 的服务器组，后续可通过 `proxy_pass http://backend` 引用。
  **负载均衡算法**（未显式指定，使用默认的 **轮询 round-robin**）：
  - 按顺序轮流将请求分发到各组内的服务器。
  - 可用的其他算法：`least_conn`（最少连接）、`ip_hash`（IP 哈希，用于会话保持）、`hash`（自定义键）等。
- **server 指令参数**：
  - `192.168.1.10:8080 weight=3`：
    `weight` 设置权重，值为 3 表示该服务器获得 3 倍的请求量（相对于 `weight=1` 的服务器）。
  - `192.168.1.11:8080`：
    默认权重 1。
  - `192.168.1.12:8080 backup`：
    标记为备份服务器。只有当所有非 backup 服务器都不可用时，才将请求转发给 backup 服务器。
  - 还可以加上 `max_fails`、`fail_timeout` 等参数控制健康检查。

### 3.5 第二个 server 块：反向代理 + 负载均衡

```nginx
server {
    listen 80;
    server_name api.example.com;

    location / {
        proxy_pass http://backend;
        proxy_set_header Host $host;
        proxy_set_header X-Real-IP $remote_addr;
    }
}
```



- **server_name api.example.com;**
  此虚拟主机只处理 `Host: api.example.com` 的请求。
- **location / { ... }**
  匹配所有 URI。
- **proxy_pass http://backend;**
  将匹配的请求代理到 `upstream backend` 定义的服务器组。
  Nginx 会根据负载均衡算法将请求转发到组内的一台服务器，并返回响应。
  **注意**：如果 `proxy_pass` 后不带 URI（如这里只有 `http://backend`），则 Nginx 会将客户端请求的完整 URI 原样传递给后端。
  例如客户端请求 `GET /users/123` → 转发给 `http://192.168.1.10:8080/users/123`。
- **proxy_set_header Host $host;**
  修改转发请求的 `Host` 头为客户端原始请求中的 `Host`（即 `api.example.com`）。
  如果不设置，后端可能收到 Nginx 本身的 IP 或主机名，导致后端应用无法正确识别虚拟主机。
- **proxy_set_header X-Real-IP $remote_addr;**
  添加一个自定义头 `X-Real-IP`，值为客户端的真实 IP（`$remote_addr`）。
  因为后端服务器直接看到的是 Nginx 的 IP（代理的 IP），通过这个头后端可以获取用户真实 IP，用于日志、地理定位、访问控制等。
  通常还会传递 `X-Forwarded-For`（包含代理链中的 IP 列表）。

------

## 4. 整体工作流程示意

1. Nginx 启动，master 进程读取配置，fork 出多个 worker 进程（数量等于 CPU 核数）。
2. Worker 进程监听 80 端口，使用 `epoll` 高效接受新连接。
3. 收到 HTTP 请求后，根据 `Host` 头选择 `server` 块：
   - 若 `Host: example.com` → 进入静态文件 server：从 `/var/www/html` 下查找文件，通过 `sendfile` 直接发送。
   - 若 `Host: api.example.com` → 进入反向代理 server：
     - 根据轮询（带权重）选择 `upstream backend` 中的一台后端服务器；
     - 添加 `X-Real-IP` 和正确的 `Host` 头；
     - 将请求转发给后端（如 `192.168.1.10:8080`）；
     - 接收后端响应，返回给客户端。
4. 所有请求和错误信息按 `main` 格式记录到 access log。

------

## 5. 实际应用建议与注意事项

- **worker_connections 调整**：
  高并发时需同时提高系统限制（`ulimit -n` 和 `sysctl net.core.somaxconn`）。例如 `worker_connections 65535`。
- **静态文件优化**：
  可增加 `open_file_cache` 指令缓存文件句柄，减少磁盘 I/O；启用 `gzip` 压缩传输。
- **反向代理优化**：
  增加 `proxy_buffering`、`proxy_buffer_size` 等指令控制缓冲；设置 `proxy_connect_timeout` 避免等待慢后端。
- **安全加固**：
  - 隐藏版本号：`server_tokens off;`
  - 限制请求方法：`if ($request_method !~ ^(GET|HEAD|POST)$) { return 405; }`
  - 限流：`limit_req_zone` 配合 `limit_req` 防止暴力攻击。
- **日志轮转**：
  配合 `logrotate` 工具自动切割日志，避免单个文件过大。

------

## 总结

这段配置展示了一个典型的 Nginx 混合部署场景：

- **前端**：托管静态网站（[example.com](https://example.com/)），高性能直接返回文件。
- **API 网关**：将 [api.example.com](https://api.example.com/) 的请求反向代理到内网三个后端服务（其中一台带权重，一台备用），实现负载均衡和高可用。

理解每一行配置的作用，是调优 Nginx 和排查问题的基础。你可以在此基础上根据实际业务需求（如 HTTPS、缓存、WebSocket 等）继续扩展。