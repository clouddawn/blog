# Dockerfile

```dockerfile
FROM harbor.cloud.weique360.com/common/nginx:v1.27.3
LABEL maintainer="weique360.com"
VOLUME /tmp
ENV LANG en_US.UTF-8
RUN echo " \
            types { \
                application/javascript mjs; \
            } \
            server {  \
                    listen       80; \
                    # nginx安全提升 \
                    server_tokens off; \
                    add_header X-Frame-Options ALLOWALL; \
                    add_header X-XSS-Protection  \"1; mode=block\"; \
                    add_header X-Content-Type-Options nosniff; \
                    # 解决Router(mode: 'history')模式下，刷新路由地址不能找到页面的问题 \
                    location / { \
                     root   /var/www/html/; \
                      index  index.html index.htm; \
                      if (!-e \$request_filename) { \
                          rewrite ^(.*)\$ /index.html?s=\$1 last; \
                          break; \
                      } \
                  } \
                  access_log  /var/log/nginx/access.log ; \
              } " > /etc/nginx/conf.d/default.conf \
    &&  mkdir  -p  /var/www \
    &&  mkdir -p /var/www/html

ADD dist/ /var/www/html/
EXPOSE 80
EXPOSE 443
```


```dockerfile
FROM harbor.cloud.weique360.com/common/nginx:v1.27.3
```

这一行是 Dockerfile 中的 **FROM** 指令，用于指定构建当前镜像时所基于的**基础镜像**。

具体解释如下：

- **harbor.cloud.weique360.com**：
  这是镜像仓库的地址，表明该镜像托管在私有 Harbor 仓库中（域名 `harbor.cloud.weique360.com`）。通常企业会搭建私有的 Docker Registry（如 Harbor）来存储和管理内部镜像，以提升拉取速度和安全性。
- **/common/nginx**：
  镜像所在的路径（项目/命名空间）。`common` 可能表示这是一个通用的、共享的基础镜像类别，`nginx` 则是镜像的名称。这种命名方式常用于多租户或多团队的镜像仓库，便于分类和权限控制。
- **v1.27.3**：
  镜像的标签（tag），指定具体版本为 `v1.27.3`。通常对应 Nginx 官方版本号。使用明确版本标签可以保证构建的可重现性，避免因基础镜像的更新（如 `latest` 标签变动）导致不可预期的行为。
- **FROM 的作用**：
  `FROM` 是 Dockerfile 中的**第一个有效指令**（可选的 `ARG` 除外）。它告诉 Docker 守护进程从指定的仓库拉取该镜像，并将其作为后续所有指令（如 `RUN`、`COPY`、`ADD`）的起点。没有 `FROM`，Docker 无法构建镜像。

因此，这一行的完整含义是：**使用私有 Harbor 仓库中 common/nginx 这个镜像的 v1.27.3 版本作为基础，来构建当前 Docker 镜像**。该基础镜像已经包含了 Nginx 1.27.3 的运行环境及默认配置，后续的 `RUN`、`ADD` 等操作将在这个 Nginx 环境之上叠加。



```dockerfile
LABEL maintainer="weique360.com"
```

这一行是 Dockerfile 中的 **LABEL** 指令，用于为生成的 Docker 镜像添加 **元数据（metadata）**，具体是设置维护者信息。

------

### 各部分组成

- **LABEL**：Dockerfile 指令，用于添加键值对形式的元数据。一个镜像可以有多个 LABEL，每个 LABEL 是一条键值对。
- **maintainer**：元数据的键（key），约定俗成表示“维护者/联系人”。
- **"weique360.com"**：对应的值（value），这里写的是一个域名或组织名称，表示该镜像的维护者是 `weique360.com` 这个团队或实体。

------

### 作用

1. **标识镜像的责任方**
   帮助用户或自动化工具了解该镜像由谁维护，便于问题反馈、安全审计或后续更新联系。

2. **可被工具读取**
   通过 `docker inspect` 命令可以查看镜像的所有 LABEL 元数据：

   ```bash
   docker inspect <镜像名或ID> --format='{{json .Config.Labels}}'
   ```

   输出会包含 `{"maintainer":"weique360.com"}`。

3. **继承与覆盖**
   当基于此镜像构建新镜像时，子镜像会继承父镜像的 LABEL。如果子镜像中再次用相同键名设置 LABEL，会覆盖原有值。



```dockerfile
VOLUME /tmp
```

`VOLUME /tmp` 是 Dockerfile 中的一个指令，用于在容器中创建一个挂载点（即目录），并将该目录标记为匿名卷（anonymous volume）。

| 组成部分 | 说明                                                         |
| -------- | ------------------------------------------------------------ |
| VOLUME   | Dockerfile 指令，用于声明容器内的一个或多个目录作为卷（volume）。 |
| /tmp     | 容器内的目标路径。该目录将变成一个卷，其内容不会被写入容器的读写层，而是存储在宿主机Docker 管理的目录中（通常位于 `/var/lib/docker/volumes/...`）。 |

## 具体作用

* 数据持久化（独立于容器生命周期）

  即使容器被删除，`/tmp` 目录中写入的数据仍然保留在卷中（除非手动删除该卷）。但需要注意的是，`/tmp` 通常存放临时文件，这里使用卷更多是为了避免容器层膨胀或实现临时文件共享。

* 绕过容器的联合文件系统

  默认情况下，容器内所有文件写入都会发生在可读写容器层。对于频繁写入或大文件写入（如临时文件、日志、缓存），可能会降低性能或导致容器层体积过大。将 `/tmp` 声明为卷可以直接写入宿主机文件系统，提升 I/O 效率。

* 实现容器间共享

  不同容器可以挂载同一个匿名卷（或具名卷），从而共享 `/tmp` 目录中的数据。不过匿名卷难以追踪，生产环境通常建议使用命名卷。

* 防止容器层存储临时数据

  某些应用会向 `/tmp` 写入大量临时数据。如果不设为卷，这些数据会随容器一起保存（即使容器停止），造成存储浪费；且 `docker commit` 会把这些临时数据也打包进新镜像。设为卷后，`/tmp` 的内容不会包含在镜像或容器层中，更清洁。

------

### 运行时行为

- **构建阶段无效**：`VOLUME` 指令在 `docker build` 过程中不会实际挂载宿主机目录。只是向镜像元数据中**声明**该目录将来应该被作为卷挂载。
- **运行阶段生效**：当使用 `docker run` 启动容器时，Docker 会自动为 `/tmp` 创建一个**匿名卷**，并挂载到容器内。除非用户用 `-v` 或 `--mount` 显式指定其他来源（如宿主机目录、命名卷），否则使用这个自动生成的匿名卷。

**示例**：

```bash
# 基于该 Dockerfile 构建镜像
docker build -t myapp .

# 运行容器，Docker 会自动为 /tmp 创建匿名卷
docker run -d myapp

# 查看匿名卷位置（可选）
docker volume ls
docker inspect <container-id> | grep -A 5 Mounts
```

### 与 `-v` / `--mount` 的关系

- 如果用户在 `docker run` 时**没有**指定 `/tmp` 的挂载，Docker 遵循 `VOLUME` 指令，自动创建匿名卷。
- 如果用户**显式挂载**了 `/tmp`（例如 `-v /host/tmp:/tmp` 或 `--mount type=bind,source=/tmp,target=/tmp`），则会覆盖 `VOLUME` 指令的默认行为，使用用户指定的源。

------

### 常见使用场景

| 场景                        | 说明                                                         |
| :-------------------------- | :----------------------------------------------------------- |
| **临时文件存储**            | 应用需要写入大量临时文件（如解压缓存、编译中间文件），使用卷可避免容器层膨胀。 |
| **日志目录**                | 某些镜像将日志写入 `/var/log` 或 `/tmp`，声明为卷便于外部收集或防止容器存储爆炸。 |
| **共享运行时数据**          | 多个容器通过挂载同一个卷来共享 `/tmp` 内容（例如任务队列、进程间通信）。 |
| **避免 docker commit 污染** | 防止临时数据被意外提交成新镜像。                             |

------

### 注意事项

1. **匿名卷不可移植**：匿名卷的宿主机路径是随机生成的，难以在容器迁移时保留数据。生产环境建议使用**命名卷**或**绑定挂载**。

2. **无法在 Dockerfile 中初始化卷内容**：`VOLUME` 声明后，后续指令（如 `RUN`、`COPY`）对 `/tmp` 的任何写入都会丢失，因为卷挂载会覆盖该目录。例如：

   ```dockerfile
   RUN echo "hello" > /tmp/test.txt   # 这一行无效，因为 /tmp 后续被声明为卷
   VOLUME /tmp
   ```

   正确做法：先声明卷，然后通过脚本在**容器启动时**（如 `ENTRYPOINT`）初始化内容。

3. **Windows 容器注意**：`VOLUME` 中的路径必须是容器内路径，且遵循操作系统的路径格式。

------

### 对比：`VOLUME` vs `-v` 挂载

| 特性       | `VOLUME /tmp`（Dockerfile） | `docker run -v /host/tmp:/tmp` |
| :--------- | :-------------------------- | :----------------------------- |
| 定义位置   | 镜像构建时                  | 容器运行时                     |
| 宿主机源   | 自动生成匿名卷（不可控）    | 用户指定（宿主机目录或命名卷） |
| 数据持久性 | 依赖匿名卷（难以管理）      | 明确可控（可备份、迁移）       |
| 可覆盖性   | 可被运行时挂载覆盖          | -                              |

------

### 最佳实践建议

- 对于需要持久化的重要数据（数据库、配置），不要在 Dockerfile 中用 `VOLUME` 声明，而应在运行时显式挂载命名卷。
- `VOLUME` 适合声明那些**无需宿主机干预**、仅用于避免容器层膨胀的临时目录（如 `/tmp`、`/scratch`）。
- 如果希望镜像开箱即用（用户不提供卷也能正常跑），`VOLUME` 是有用的默认行为。

------

### 总结

> **VOLUME /tmp** 声明了容器内的 `/tmp` 目录应该被创建为一个匿名卷，目的是防止临时数据写入容器层，提升 I/O 性能并避免容器存储膨胀。其实际挂载行为发生在容器运行时，用户可以通过 `-v` 或 `--mount` 覆盖这一默认行为。























