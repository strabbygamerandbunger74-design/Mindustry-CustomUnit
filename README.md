# Mindustry-CustomUnit

一个允许玩家创建自定义单位的Mindustry模组，基于官方Java模组模板开发。

## 功能介绍

- 允许玩家创建自定义单位
- 支持自定义单位的属性和行为
- 提供直观的单位编辑器界面
- 兼容Android和PC平台

## 构建说明

### 桌面测试构建

1. 安装JDK **17**。
2. 运行 `gradlew jar` [1]。
3. 模组jar文件将在 `build/libs` 目录中。**仅使用此版本进行桌面测试。它不适用于Android。**

### 通过Github Actions构建

本仓库已配置Github Actions CI，每次提交时自动构建模组。要获取适用于所有平台的jar文件，请执行以下操作：

1. 将仓库推送到Github。
2. 检查仓库页面上的"Actions"选项卡。选择列表中最近的提交。
3. 如果构建成功，"Artifacts"部分下应该有一个下载链接。
4. 点击下载链接（应为仓库名称）。
5. 解压下载的zip文件，其中包含可用于Android和桌面的模组jar文件。

### 本地构建（Android兼容版本）

本地构建需要更多时间设置，但如果您之前做过Android开发，应该不会有问题。

1. 下载Android SDK，解压并将 `ANDROID_HOME` 环境变量设置为其位置。
2. 确保您已安装API级别30，以及任何最新版本的构建工具（例如30.0.1）
3. 将build-tools文件夹添加到PATH中。例如，如果您安装了 `30.0.1`，则应为 `$ANDROID_HOME/build-tools/30.0.1`。
4. 运行 `gradlew deploy`。如果一切正确，这将在 `build/libs` 目录中创建一个可在Android和桌面端运行的jar文件。

## 添加依赖

请注意，所有对Mindustry、Arc或其子模块的依赖**必须在Gradle中声明为compileOnly**。切勿将 `implementation` 用于核心Mindustry或Arc依赖。

- `implementation` **将整个依赖项放入jar中**，这在大多数模组依赖项中是非常不可取的。您不希望Mindustry API的全部内容都包含在您的模组中。
- `compileOnly` 意味着依赖项仅在编译时存在，不包含在jar中。

只有当您想将另一个Java库*与您的模组一起打包*，并且该库不存在于Mindustry中时，才使用 `implementation`。

---

*[1]* *在Linux/Mac上是 `./gradlew`，但如果您使用Linux，我假设您知道如何正确运行可执行文件。*
