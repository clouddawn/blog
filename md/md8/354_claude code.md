# claude code

https://my.feishu.cn/wiki/Takxwov60iO5OOkOmpEcpOGynac

# 一、初步上手

## 1. 部署前准备

首先需要下载和安装一个 **Agent IDE**（智能体集成开发环境）。

推荐使用以下免费IDE，无需购买会员，使用免费额度即可完成后续CC部署：

| **Agent IDE**                          | **下载地址**                                    |
| :------------------------------------- | :---------------------------------------------- |
| Cursor                                 | [官网下载](https://cursor.com/cn/download)      |
| Google Anti-gravity                    | [官网下载](https://antigravity.google/download) |
| Trae                                   | [官网下载（cn）](https://www.trae.cn/)          |
| [官网下载（en）](https://www.trae.ai/) |                                                 |

以 **Cursor** 为例，下载进入后，可以构建如图的开发环境布局：

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=YWFmM2Y2N2Y3NzhjOTM0ZGQ1NTM2ZWY1OWI0NzU2YjRfSmkzbHlORmpoUUdqYzBnekd5R01jZ3pnVDlZNk1zYURfVG9rZW46U2J6cmJsYWhXb1NRYUl4bE9mS2NnZjJObjZjXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)



## 2. 安装Claude Code

### **方式 1：终端命令行安装**（需魔法上网）

根据自身系统，选择对应代码，在IDE终端输入并回车：

#### **Windows：**

**步骤 1：**在ide终端用WinGet先安装Git，遇到选项直接输入`y`（yes）

```Plain
winget install Git.Git
```

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NzMyNzNjZjQzY2Y4M2UzZGY0NWNlMjAzYjU3ZmM5YmNfRWYxVUNMR0x2aHBZc0ZNbjdCMmkweHdTVWxjTktkRlBfVG9rZW46R1NwU2JGUGR3b05Mck14c1RoRmNvSEZqbndlXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤 2**：在ide终端输入代码，下载Claude code

- **Windows - PowerShell（ide终端默认用这个）：**

```Plain
irm https://claude.ai/install.ps1 | iex
```

- **Windows - CMD：**

```Plain
curl -fsSL https://claude.ai/install.cmd -o install.cmd && install.cmd && del install.cmd
```

- 下载好以后进行版本验证，**版本号正常显示，代表安装完成！**

```Plain
claude --version
```



#### **macOS：**

- 直接在ide终端输入以下代码

```Plain
curl -fsSL https://claude.ai/install.sh | bash
```

- 下载好以后进行版本验证，**版本号正常显示，代表安装完成！**

```Plain
claude --version
```

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NWNhODU0MDgwYTM5MzI3ZGQxYmZkM2YzZDFkYzM0ODJfQThDYmNTVzl0SzlSWDQ3bVVwNHM4QWVQVnJCbXloTzZfVG9rZW46S2VFNGJQSzlWb3l0czl4cEd4eGNadnVFbm5oXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

### **方式 2：Agent原生安装（需魔法上网）**

**步骤 1：**直接向IDE Agent输入提示词：

```Plain
帮我安装node并且用npm安装好最新的claude code
```

**步骤 2：**验证Claude code版本号，确认安装成功

```Plain
claude --version
```



### **方式 3：无魔法安装Claude code**

#### **Windows：**

**步骤 1：**用WinGet先安装Git，遇到选项直接y（yes）

```Plain
winget install Git.Git
```

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=YTJlN2Q3ZjdkODFmYTRmY2ExYjZkMmQ5MjllZDkxOWZfOXRacVA4dFV2THY3eVNldkFyeWo3UU5hcUpPSjhTeXJfVG9rZW46TExpV2J1OXJZb0ZtaFl4Z2h4Q2NDRnhsbmNoXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤 2**：在ide agent输入以下提示词，让agent一条龙搞定Claude code安装

```Plain
执行这条代码安装Claude code：winget install Anthropic.ClaudeCode
安装完后，把Claude Code的可执行文件路径配置到系统环境变量的Path里。
```

**步骤 3**：装完后，重启ide，验证Claude code版本号，确认安装成功

```Plain
claude --version
```

#### **macOS：**

**步骤 1**：在ide终端先装Homebrew

```Plain
/bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)"
```

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=MzI0ZGMwNjFkNGU3ZjMzMDQ4MDBjNTExOWU2NGY2ZmFfZVBKbEhNcEFmVTZIcU1MSWpvOHVaUTdKMkJEbXR2MVhfVG9rZW46RWEzd2JTSGxVb2RkMUJ4bnFvWWNKbnhWbkxnXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤 2**：向ide agent输入提示词：

```Plain
帮我把homebrew加到PATH路径变量里面去
```

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=MzI5Y2M0MzYzYWVlZWFiYjBmNjljNTQyZmQ4MTU3NThfSVlKSEZ4R2hkNWVTY0I1dHNwU0UxS0xha3RHVnAwR1RfVG9rZW46R0dES2JHbVFGb1pJck14RFFDYmNzT1F6bkdlXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤 3**：在ide终端输入代码，安装Claude Code

```Plain
brew install --cask claude-code@latest
```

**步骤 4：**验证Claude code版本号，确认安装成功

```Plain
claude --version
```



## 3. 配置大模型

1. 下载CC Switch做多模型切换和管理
   1. **CC Switch的GitHub仓库下载页：****https://github.com/farion1231/cc-switch/releases/tag/v3.14.1**

   2. **最新版本号：**v3.14.1

**步骤1：**在下载页，根据系统选择对应下载包：

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=MGNkNTgyOWQ5YWIxOTg4N2Y2NzI4NjViNDE4YjA5NGNfQTJ0T1F5MmhGb0VaMnRvOGxUZDhYM2F1clh5WkJGNGxfVG9rZW46V0xIUWJhSkRab3JSanR4M2Q5VmNSanYybnhkXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤2：**安装完成后，**务必在打开Claude Code之前**，优先设置CC Switch。在CC Switch的Claude Code页面添加API Key供应商：

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NWZkNGNmM2UwMWIzODVkYmJlMDE2ODQ4ODU1NmQxZWZfT2hYbDBtVUY5clNCSXJHWTFaSUF2WmNRYXU3Y3BaUHZfVG9rZW46WjBxVmJoUlR6bzBSS3h4d00yaGNhenF3blZmXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤3：**以 **Minimax** 为例，选择对应厂商（中国版），然后填写API Key和Base URL：

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=MmU4NWQ0MGMyOThhYWY3NDNlOThjMWQxNTIzYzc1NWVfSGdGWGpNcDJJUmQ5d0FCWkZTMVZkTGxzdXg3WE00M29fVG9rZW46VDdkd2JRcFFub0xXcmp4a3FJZmN6a1FybjFkXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=MzlhOWRiMWQyZGQyNWFmZDRhZWViNTc2MzE0MzViNzJfdVg4b2FKbzZ1TmJRWHhsTDdIWFBUMFNjck1JaGxwVWlfVG9rZW46VEZWUWJWbHNpb0JtUjJ4ZzdKbWN4MGh5bmhxXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)



> - 如果不知道Base URL，可以在API Key的官方文档里找到（以[Minimax的官方文档](https://platform.minimaxi.com/docs/guides/models-intro)为例）
>
> ![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NjMxZGVjNzMzYzc3MjQwNDI2NGQ2MjQwOTQzODE5ODJfYWZOa0RhYnExeWRWWXhaaUl5aVVtMkdZZFZlMmViUmFfVG9rZW46QkN1UWJEalIxb2FSOWt4U1RBM2MxeEdSbmNiXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤4：**选择「启用」设置好的API，CC的大模型配置完成！下一步可以准备打开Claude Code了：

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=N2MxOTBjN2I1MDAwYzkyZWY0OWM2NWE3NDM3NGM5YjRfeGZLMnNyajhlWDVpZENJYnc3U0ZFT1d5eHFJNGFmUkZfVG9rZW46VHlQbmJXQ25Db0ZOQkh4OGd0UmNmaDI2blRkXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)



## 4. 基础实操

**步骤1：**在IDE终端打开CC，输入：

```Plain
claude
```

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NWY2MjE1ZTQwODY5YTM1ZmM2MzdlZGYyNTNhNzZjZDVfamQ2UjBWbnVjb0Q4Q3EzcHY3ZUtkU3YxZTZPWUxLd1RfVG9rZW46SVFEcGI2ZU1Mb0I1aDd4RGdudGM3QzJNbkJnXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=YTU1OTZiMmIxMmI0OWFkOWY0YTViMWE2NTNlYjkwZjFfNHBjNEg1SUdEcXVNV0RIS29WQ2d3UlRYOG9uTDRvQVlfVG9rZW46RkhUV2JMdlVxb3pSaDd4d0dxemNrNExkbkFIXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)





**步骤2：**根据个人喜好设置皮肤与主题，然后一路 `yes` 后，进入CC主界面：

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=YzUzODdkYTVmMjJiZjNkMTY2MjRmYzUxOGY0OWY1YjBfNnZrdTFJZTM2elk2aGRUNjRTUHNmc0wxZXBoYzFtQTVfVG9rZW46Q0Z1amIxbjl1b3RTb054UG84T2Myc0lObm9jXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤3：**默认情况下，CC接到任务后会进入 **计划模式（Plan Mode）**：

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=YTU2MjhjMjlhZmI2ZmU1ZjllNmRkNjAyM2UyODljNmNfQlZlTlE5TWFHMDVXclNnWEZaZlNTNE1yUGZjdXcySjJfVG9rZW46VVhFNWJDVmhFbzQ2WFZ4dWFQbmNVcnF2bk40XzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤4：**使用shift+tab，可以让CC在计划模式、默认模式和Accept Edits模式之间来回切换

| 模式             | 功能                                                         |
| :--------------- | :----------------------------------------------------------- |
| 默认模式         | 启动 Claude Code 后的初始交互状态，类似于一个增强版的对话终端，用于意图确认、信息查询和简单任务。 |
| 计划模式         | Claude 进行复杂的代码更改时，它会进入这一阶段。分析需求并制定执行步骤。不直接动代码。 |
| Accept Edits模式 | 这是 Claude Code 的“落地”阶段，会执行代码变更的最终确认与写入 |

额外提醒：

1. 如果希望CC能一路绿灯执行所有操作，需要输入指令`/exit` 退出重启后，在启动CC时输入以下命令

```Plain
claude --dangerously-skip-permissions
```

1. CC在Accept Edits模式下，执行终端命令时，下图三个选项的含义依次分别是：
   1. **仅同意这一次**的命令执行
   2. **同意**，且该项目之后执行项目依赖安装时，不再询问
   3. **不同意**，再商量
   4. ![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NmU3NTAwY2MwM2MzYzdkZmM4ODBiMGI1NDUwOWRmYzdfUXRSaWJpNzVXUDc3dHJxNjlyQ3RoeVMya2IyMUYyNThfVG9rZW46QWwxU2Jxa3Q1b203cjl4VGE5VWNiN0hhbmFiXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)



## 5. 如何提供文件给CC

### **方式 1：本地文件**

使用 `@` 指令让CC进行本地文件信息查找：

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=ODE4MjgzNzkyNzM5N2RhYzMzMWI4NmUwZDE2ZTZmYWNfaGtoZ2tDQ29BSDRPU2NVZ29IZ1BRd2dBM0ZFdU4yS3lfVG9rZW46WFRWT2JFc2llb3ZOUnN4aWt5U2NDVUF2bklnXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

### **方式 2：图片**

直接拖拽图片至对话框，或复制/粘贴：

- **Windows：**`Alt + V`
- **macOS：**`Command + V`

### **方式 3：多行文本输入**

在CC文本框内换行的快捷键（**不是** Shift + Enter）：

- **Windows：**`Ctrl + Enter`
- **macOS：**`Option + Enter`



## 6. 指令大全

| Claude指令  | 功能说明                                                     |
| :---------- | :----------------------------------------------------------- |
| `/help`     | 提供所有指令，以及指令背后遵循的意思                         |
| `/model`    | 切换高中低档模型                                             |
| `/btw`      | By the way缩写，可以暂时切出正在执行的项目，隔离上下文，方便使用者与CC进行临时对话。会话完毕后，可按esc消除临时会话 |
| `/simplify` | 输入后会派生出3个agent，从代码质量、运行效率和复用性三个角度做一次代码审核，然后自动优化修改 |
| `/rewind`   | 进入回滚界面                                                 |
| `/compact`  | 主动压缩精简上下文                                           |
| `/clear`    | 彻底清空上下文，相当于重开一个会话                           |
| `/context`  | 详细展示agent当前的上下文信息，诸如：上下文占比，上下文类别等等 |
| `/resume`   | 在全新的上下文窗口，选择恢复到之前的对话                     |
| `/init`     | 初始化创建项目级Claude.md                                    |
| `/memory`   | 针对Claude的全局、项目记忆，以及auto memory进行操作和管理    |
| `/agents`   | 创建、调用、管理子agent                                      |
| `/plugin`   | 发现新插件，管理已下载插件，新增插件生态                     |

  更多指令可参考以下pdf文档：

暂时无法在飞书文档外展示此内容



# 二、掌控与管理

## 1. Git下载与设置

在CC中输入以下提示词，根据CC引导进行操作：

```Plain
帮我下载Git，并与我的GitHub账号绑定
```



## 2.上下文管理

**步骤1:**确认上下文进度

- 输入`/context`命令，它会详细的展示我们的上下文占比信息：
  - ```Plain
    /context
    ```

  - ![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2IyYWM0MWJjMzA2YzFmYTExMWU5NmFhZDMxZDNkNGNfdkxENUhMNDVqdEpxVmdyVGNtN25JcFlwZHFJUVE1ZWNfVG9rZW46SlYwM2IycXBqb005R2J4cjFIaWMzRWpibmFlXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤2:**主动压缩上下文

- cc会在上下文即将满的时候，会帮我们自动压缩
- 我的习惯是看到高于60%了，就大概率需要 `/compact` 

```Plain
/compact
```

**步骤3:**彻底清空上下文

```Plain
/clear
```

**步骤4:**context占用条常驻

- 对CC输入提示词，并根据CC引导完成后重启终端即可：
  - ```Plain
    帮我配一个 statusLine,显示当前目录+模型+上下文剩余百分比 
    ```

  - ![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjA5NGRkYTA1MGJhMTM5ZjMyZTg3YmNjZTg1M2Q1MThfZDFQdDNac3Z6UUlJc294SE1YMDcyYVZXcEhOQVhXY3JfVG9rZW46RjFDMmJNbTVNb2hqaWF4dnJ2M2N3WktkbnVlXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤5:**对话恢复

- 输入以下指令后，选择恢复到你想要的会话即可：
  - ```Plain
    /resume
    ```



# 三、个性化

## 1. Claude.md 配置

**项目级 Claude.md** 创建方式：

```Plain
/init
```

**全局级 Claude.md** 有两种创建方式：

**方式 1：提示词交互**

```Plain
记得永远说中文，写进全局claude.md
```

**方式 2：使用指令**

输入 `/memory` 后，选择「User Memory」进入：

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NjIwMThlMWE4Y2U3MzFhNWQyMDBiNzZhMTg4Yzc4YjNfYVdHNnZGSlRxdlJ1TG9NV1VoaExZR2JiU2Y0Wm1hd2FfVG9rZW46UEF0SmJOdGNybzhremN4YjhPRmNhQmlEblBkXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)



## 2. Auto Memory

- 打开Auto Memory：输入`/memory` ，选择「**Auto-memory**」并输入回车开启
  - ![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=OTk2MTE4ZDIyNTYyNzM1ZGJjNjI1ODk2YmI0MjA3ZDFfREE0T1Exd0lNNUpBSDFqQ1FTWjF6OVVLTFpqTnp4WGxfVG9rZW46TG1sWGJCNGpLb2NnS3R4Zm84Q2NxNTJCblJmXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

  - > 打开以后，我们与CC的工作交互过程中，那些没有显式的主动写进claude.md的一些习惯、错误、经验，都会以自动记忆形式被记录，但仅限于当前项目，不会跨项目产生影响。

# 四、能力扩展

## 1. Skill 技能扩展

1. **Claude Code优质skill推荐**

   1. 可以将skill链接给cc，让cc帮你直接下好

   2. | skill名称        | 功能                                                       | 下载链接                                                     |
      | :--------------- | :--------------------------------------------------------- | :----------------------------------------------------------- |
      | Find-Skill       | 根据用户需求，查找和安装来自agent skill开放生态的技能      | [GitHub](https://github.com/vercel-labs/skills/tree/main/skills/find-skills) |
      | Frontend- Design | 创建具有独特风格、生产级品质且设计精良的前端界面           | [GitHub](https://github.com/anthropics/skills/tree/main/skills/frontend-design) |
      | Skill- Creator   | 创建新skill、修改和改进现有skill，并衡量skill表现          | [GitHub](https://github.com/anthropics/skills/tree/main/skills/skill-creator) |
      | 卡帕西skill      | 一个依据卡帕西经验总结，用于提升Claude Code编码表现的skill | [GitHub](https://github.com/forrestchang/andrej-karpathy-skills) |

2. **skill合集网站：****lobehub**

   1. 大家既可以根据分类去寻找自己需要的skill，也可以直接在精选合集查看推荐的优质skill
   2. ![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2I3MzUzY2E3YzE4OTM0OTExZGM0MzhlMjdjMjM2NmRfTThQMGFieGpRY3RBSTQ5QWdCaEFaTnBuOUJQSTRpd05fVG9rZW46T01wMmJZTGFub1I3WkJ4MWZiVmNYV01TbnI4XzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

3. **想创建自己的skill？**

   1. 我们还有一份网页版教学文档，非常详细：[Agent Skills指南（Claude Code版）](https://ccnk05wgo092.aiforce.cloud/spark/faas/app_4jdqh6vm3jpdp)

4. **下载了skill怎么装？**

   1. 可根据需求，将skill文件放入**项目级skill**与**全局级skill**的存放**文件夹**
   2. ![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=Zjg2MGE3ZWVjYWY1YmY1NjJjNGU4NjIzNDJhODgzMWRfRkdraFVNZFFremJtSFZXZkRtd1E4M0xpR1ozbUU3YVZfVG9rZW46T2U1TGJGWU12b0htTGl4dHJySGNhVUloblBlXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)



## 2. MCP 扩展

关于MCP的部分，可结合以下教程进行学习与实践：

**学习资源**

📺 **视频教程：**[用神器Claude Code！打造贴身AI秘书团【小白教程】](https://www.bilibili.com/video/BV1zqeMzfEiQ/?spm_id_from=333.1387.upload.video_card.click&vd_source=b82dea39967bb9f5eb44be501b4cae31)

📄 **文档教程：**[Claude Code教程](https://my.feishu.cn/wiki/BxLTwlkvkiQhJkkJ7vgc95aZnMe)



## 3. CLI 命令行工具

**推荐几个优质CLI，**直接将下载链接给CC，让CC全权负责下载和引导操作：

| **CLI名称** | **功能**                                                     | **下载**                                                     |
| :---------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 飞书CLI     | 飞书官方CLI工具，覆盖消息、文档、多维表格、电子表格、幻灯片、日历、邮箱、任务、会议等核心业务域，提供200+命令及24个AI Agent Skills | [GitHub](https://github.com/larksuite/cli/blob/main/README.zh.md) |
| OpenCLI     | 万能命令行工具箱，通用命令行中心与AI原生运行平台，能将任何网站、桌面应用或本地程序变成统一命令行操作界面 | [GitHub](https://github.com/jackwener/opencli)               |
| CLI         | GitHub 的官方命令行工具。它将拉取请求、问题和其他 GitHub 概念带到终端中，与你已经在使用 `git` 和代码的地方并排显示。 | [GitHub](https://github.com/cli/cli)                         |
| gemini-CLI  | Gemini CLI 可将 Gemini 的功能直接引入终端。它提供轻量级的 Gemini 访问方式，能够以最直接的方式从终端命令访问 Gemini 模型。 | [GitHub](https://github.com/google-gemini/gemini-cli)        |

> 给大家推荐一个GitHub上的CLI主题推荐网页，大家可按需查找自己想要的CLI：[Command-line interface](https://github.com/topics/cli)



## 4. 子Agent（SubAgent）

**创建子Agent的两种方式：**

1. **自动触发：**任务复杂且存在并行可能时，CC会自动派生子Agent并行推进
2. **手动创建：**通过指令 `/agents` ，在Library界面进行创建
   1. ![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=YmVmMWRkYTg2YTE1YWRlZGZiN2ZmZjRkYmRlYzI1MTBfUW1jTFRZUDBDZ2pJMVcyaVhnSjA3S1ZyWkx2NXRMNGhfVG9rZW46SnF3RWJXeDFQbzZKQmR4d3d5UmNwbHExbjRlXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**手动创建步骤：**

**步骤1：**选择创建项目级或全局级子Agent

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=OWUzNzViNThmMDA1YmVjNzJmMGJhM2JmYWY5YTBlY2JfbkRmZGN3cXQwb2U1NlBpWkhIZGpyNkxiVVZobm1EdWJfVG9rZW46UWE2emJXbEZFb24wUFZ4c1dpamNUcVMxbnloXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤2：**选择「AI辅助创建」，让AI根据意图辅助创建

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=Y2VhYmUyYTNjNDMxNWQzZGIyMzdkNDMyNWRhZWM3MTBfZGx1SldJaGxvQUZka3N6c21UODg1WmJHc2dnTlZNRENfVG9rZW46RzZUa2JROFNqbzJjRUF4bGswTmNsN0JtbkpnXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤3：**描述想要的子Agent功能

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=Mzk5Y2Q3MjRmYTA4NzczMWIyMjY2ZGVkMWNkZWQyMzdfTEhpUmNVY3g0ZzRwUGdDUGoyOUo1ZndLaDl0RHZEWmZfVG9rZW46VVdVRGJTMmg4b3lLWXF4b2NtbmNQZ3ZKbk5LXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤4：**决定子Agent工具权限（✓为选中）

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=MzdmYTU1ZTM0NzZiNDZmOTczZjg1MjE1MjZiYTY5ZmVfcXVzclNTZFMxR3FGOENBYzRiMmZUTElLdnVwMXZ3R21fVG9rZW46STNQQmJ4b3h3bzdNZ0l4eHZkdWNFbjFybnpoXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤5：**选择Claude的模型

- 一般选Sonnet就可以（如果使用CC Switch配置了模型，选哪个都一样）
  - ![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=ZjQ4NTNhYTExY2IxMzFhMTQ0Nzc4YWZiZWEyZGNjMjhfdVo3a0tZMDFaME1BNjhlNDgyQTNMOTNoSnRMb2tkOWJfVG9rZW46RWduY2IxeHZ1b0NNOGF4R1NwemNBbGtZbmJoXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤6：**为子Agent挑选区别于主Agent的颜色

- 选个好看的颜色
  - ![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NTg5YzI1ZmY1YWM2MzBmNTE0MzQ2MTRhYjE2NDRmOWRfOUFuVjdabVFQMFVRZEhBNnFXVDhaclRLM1hXc3h3RkhfVG9rZW46VlJTS2JtcFJpbzJwS2Z4Mnk2QWN3SHNHbk1iXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤7:**调用与管理子Agent

- 输入 `/agents`，在Library下选择已创建的项目级子Agent
  - ![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NDVmMjZjODIzYTE3MTU2MGZmZDIxZTBlYjBiNmExYzFfZEc5TVRkZG1KZ3FKUFl6UlVjZDViNkpibXlVMkxJOEhfVG9rZW46T0dZYWI4WlNXbzQybUF4NEUycmMwQ1NmbndjXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)
- 根据需求对子Agent进行相应操作
  - ![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=MjgyYTk1NjFmNzc0NGJmZmYwMmFjNjdkOTIwZmQxYWZfMWpHenZMT0d1c0l0SFkxWHNRQ3hHOVpObmhiWDh1d1ZfVG9rZW46VXA3TGJweUlVb01GMWd4cVNNSmMxMTRGbmhmXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)



## 5. Hook 钩子

推荐以下Hook设置，直接告诉CC帮忙设置：

```Plain
设置一个hook，每次完成任务之后，都自动执行一个声音脚本，发出一个提示音"叮"进行提醒
设置一个hook，每次提交代码之前，都会自动触发代码格式的检查
```



## 6. 插件（Plugin）

**插件说明**

插件是打包了 **Skill**、**SubAgent**、**Hook**、**MCP** 的整合性概念

**步骤1：**通过指令 `/plugin` 进入插件管理界面

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=ZmVjYTdkNWI5MDM4MTdkYzljNzJlOTI2NjJhOTdkNGNfdFVNVFdwRmtSRFh0dDBFU1ZseURKd0FXdzZIa2w0UTZfVG9rZW46UjlNaGJvWUhUb2hXd3p4Y2lydGNxbVUzbkVkXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)

**步骤2：**在插件管理界面，可以收录下载钟意的插件，或管理已下载插件

![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=ZWQ3ODMyYzMxZDQ0MGJhMDUxZWU2ZWFjNjc0N2QwYzZfa01iT21KQnU1MXdKd1ZWTXRyWDN1VWdTeTNIeXNsZk1fVG9rZW46U1BaZWJnRlVYbzhYTnF4QTFmQ2NFN3NXbkJjXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)![img](https://my.feishu.cn/space/api/box/stream/download/asynccode/?code=NDVmNzU4YzhjN2VmMjM5ZGM2ODBlM2FlNmM3NjA4NjFfSUowMTlaSGM4cWFjZWN6TnZJbERqWXpvRW00TnFWM05fVG9rZW46RXZaZ2JncjRrb3NzSzV4amU3Y2NweXRmbndiXzE3ODQ3MDY1MzM6MTc4NDcxMDEzM19WNA&add_watermark=true&scene_type=CCM)





推荐给大家一些Claude Code官方精选的一些插件：

| 插件名称          | 插件功能                                                     | 链接                                                         |
| :---------------- | :----------------------------------------------------------- | :----------------------------------------------------------- |
| commit-commands   | 使用简单的命令简化 Git 工作流程，包括提交、推送和创建拉取请求 | [GitHub](https://github.com/anthropics/claude-code/tree/main/plugins/commit-commands?utm_source=claudecodeplugins.dev) |
| content-creator   | 这位内容创作者擅长跨平台内容创作，从长篇博客文章到引人入胜的视频脚本和社交媒体内容，无所不包。 | [GitHub](https://github.com/ccplugins/awesome-claude-code-plugins/tree/main/plugins/content-creator?utm_source=claudecodeplugins.dev) |
| security-guidance | 安全提醒钩子，在编辑文件时提示潜在的安全问题，包含命令注入、XSS 及不安全的代码模式 | [GitHub](https://github.com/anthropics/claude-code/tree/main/plugins/security-guidance?utm_source=claudecodeplugins.dev) |

如果仍有需求，可以去官方/三方插件网站继续查看自己需要的插件：[Plugins](https://claude.com/plugins#plugins) / [Claude Code Plugins](https://claudecodeplugins.dev/zh)