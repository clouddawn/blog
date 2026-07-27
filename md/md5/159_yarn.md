# yarn

* Yarn 是代码的包管理器。它允许您与来自世界各地的其他开发人员一起使用和共享代码。
* 代码通过称为**包的**东西共享。一个包包含所有共享的代码以及一个描述该包的`package.json`文件（称为**清单**）。

### 全局安装

```bash
npm install -g yarn
```

### 更新到最新版本

如果您以后想将 Yarn 更新到最新版本，只需运行：

```bash
yarn set version latest
```

## 用法

#### 开始一个新项目

```bash
yarn init
```

#### 安装所有依赖

```bash
yarn install
```

#### 添加依赖

```bash
yarn add [package]
yarn add [package]@[version]
```

#### 向不同类别的依赖项添加依赖项

```bash
yarn add [package] --dev  # dev dependencies
yarn add [package] --peer # peer dependencies
```

#### 升级依赖

```bash
yarn up [package]
yarn up [package]@[version]
```

#### 删除依赖项

```bash
yarn remove [package]
```



