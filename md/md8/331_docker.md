# Docker

Docker 是一个开源的容器化平台，它让开发者可以将应用及其依赖环境打包成一个轻量级、可移植的容器，从而实现一次构建，到处运行。

## 核心概念

| 概念               | 说明                                                         | 类比               |
| ------------------ | ------------------------------------------------------------ | ------------------ |
| 镜像（Image）      | 只读模版，包含应用运行所需的一切（代码、运行时、库、配置）   | 面向对象中的类     |
| 容器（Container）  | 镜像的运行实例，是隔离的进程，有自己的文件系统、网络、进程空间 | 面向对象中的对象   |
| 仓库（Repository） | 存储和分发镜像的地方（如 Docker Hub、Harbor）                | 代码仓库（GitHub） |
| Dockerfile         | 定义如何构建镜像的脚本，每条指令创建一个镜像层               | 配方 / 构建说明书  |

## 架构

Docker 采用 客户端-服务端 架构：

* Docker 客户端：用户使用的 `docker` 命令（如 `docker run` 、`docker build`）。
* Docker 守护进程：负责管理镜像、容器、网络、存储卷。监听 REST API 请求。
* Registry：镜像仓库。默认公共仓库为 Docker Hub，也可搭建私有仓库（如 Harbor）。

用户通过客户端向守护进程发送指令，守护进程与仓库交互（拉取/推送镜像），并管理本地容器生命周期。

------

## Docker 的优势

| 优势                 | 描述                                                         |
| :------------------- | :----------------------------------------------------------- |
| **环境一致性**       | 开发、测试、生产环境相同，消除“在我机器上能跑”的问题。       |
| **轻量高效**         | 容器共享宿主机内核，无需模拟完整操作系统，启动毫秒级，资源占用远小于虚拟机。 |
| **可移植性**         | 镜像可在任何支持 Docker 的 Linux/Windows/macOS 服务器上运行，云平台、物理机均可。 |
| **版本控制与 CI/CD** | 镜像可像代码一样进行版本管理，支持自动化构建、测试、部署。   |
| **资源隔离**         | 利用 Linux 内核的 Namespace 和 Cgroups，实现进程、网络、文件系统隔离，安全可控。 |
| **快速交付**         | 通过 Dockerfile 和镜像分层，构建、分发、更新非常迅速。       |

**与虚拟机对比：**

| 特性     | Docker 容器                  | 传统虚拟机                       |
| :------- | :--------------------------- | :------------------------------- |
| 启动速度 | 毫秒~秒级                    | 分钟级                           |
| 磁盘占用 | MB~GB（共享基础镜像层）      | GB~TB（每个虚拟机完整OS）        |
| 性能损耗 | 几乎无（直接使用宿主机内核） | 较大（需模拟硬件、运行Guest OS） |
| 隔离级别 | 进程级                       | 系统级（完整OS）                 |
| 数量     | 单机可运行成百上千个         | 通常十几个                       |

------

## 常用命令

```dockerfile
# 镜像相关
docker pull nginx:1.27          # 拉取镜像
docker build -t my-app .        # 从 Dockerfile 构建镜像
docker images                   # 列出本地镜像
docker rmi <image-id>           # 删除镜像

# 容器相关
docker run -d -p 80:80 nginx    # 后台运行容器，映射端口
docker ps                       # 查看运行中的容器
docker stop <container-id>      # 停止容器
docker rm <container-id>        # 删除容器
docker exec -it <id> bash       # 进入容器内部

# 仓库相关
docker tag my-app myrepo/my-app:v1
docker push myrepo/my-app:v1    # 推送到私有仓库
```

------

## 工作流程示例（前端 + Nginx）

```dockerfile
# Dockerfile
FROM nginx:1.27
COPY dist/ /usr/share/nginx/html
EXPOSE 80
```



```dockerfile
docker build -t my-frontend .
docker run -d -p 8080:80 my-frontend
```



访问 `http://localhost:8080` 即可看到前端页面。

------

##  生态系统

- **Docker Compose**：定义和运行多容器应用（如前端 + 后端 + 数据库）。
- **Docker Swarm**：Docker 原生容器编排工具（已被 Kubernetes 更广泛应用）。
- **Kubernetes**：目前主流的容器编排平台，可以管理数千个 Docker 容器。
- **Harbor / Docker Hub**：镜像仓库，支持存储、扫描漏洞、访问控制。

------

## 总结

> **Docker 是一种容器化技术，它将应用及其依赖打包成标准化的镜像，通过隔离、轻量的容器来运行，彻底改变了软件的打包、交付和运行方式。** 无论你是开发、测试还是运维人员，Docker 都能帮助你实现环境一致性、快速部署和高效资源利用。现在它已成为云原生时代的基础设施核心组件。