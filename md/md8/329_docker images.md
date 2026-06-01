# docker images

`docker images` 是 Docker 中用于列出本地已下载或构建的镜像的基础命令。简单说，它就像你电脑上的相册，展示了所有存储在本地 Docker 引擎中的镜像。

## 命令格式与基础用法

```bash
docker images [选项] [仓库名]
```

默认输出（不加任何选项）会展示一个表格，包含一下关键信息：

| 列名           | 说明                       | 示例                       |
| :------------- | :------------------------- | :------------------------- |
| **REPOSITORY** | 镜像所属的仓库名称         | `nginx`, `myapp`, `ubuntu` |
| **TAG**        | 镜像的标签（版本标识）     | `latest`, `1.21`, `20.04`  |
| **IMAGE ID**   | 镜像唯一标识符（前12位）   | `f0b7a5b3e4c1`             |
| **CREATED**    | 镜像创建的时间（相对时间） | `2 weeks ago`              |
| **SIZE**       | 镜像占用的磁盘空间大小     | `133MB`                    |

> 如果你运行 `docker images`，可能会看到类似下面的输出：
>
> text
>
> ```
> REPOSITORY   TAG       IMAGE ID       CREATED        SIZE
> nginx        latest    f0b7a5b3e4c1   2 weeks ago    133MB
> myapp        1.0       9a8c7b6d5e4f   3 days ago     850MB
> ```

