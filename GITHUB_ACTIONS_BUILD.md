# GitHub Actions 在线编译 APK

这个项目已经带有 GitHub Actions 配置：

```text
.github/workflows/build.yml
```

上传到 GitHub 仓库后，可以直接在线编译 debug APK。

## 手机操作步骤

1. 打开 GitHub，新建仓库，例如：

```text
Ace6IPhoneSpoof
```

2. 解压本项目压缩包。

3. 上传解压后的项目内容到仓库根目录。

仓库根目录应该能看到这些内容：

```text
.github/
app/
build.gradle
settings.gradle
gradle.properties
README.md
GITHUB_ACTIONS_BUILD.md
```

注意：不要只上传 zip 文件本身，GitHub Actions 需要看到解压后的源码文件。

4. 打开仓库顶部的：

```text
Actions
```

5. 选择左侧或列表里的：

```text
Build APK
```

6. 如果没有自动运行，点击：

```text
Run workflow
```

然后确认运行。

7. 等待任务变成绿色成功。

8. 点进成功的运行记录，在页面底部找到：

```text
Artifacts
```

下载：

```text
Ace6IPhoneSpoof-debug-apk
```

9. 下载后解压 artifact，里面会有：

```text
app-debug.apk
```

安装这个 APK，然后去 LSPosed 启用模块和选择作用域。

## 如果编译失败

点进失败的 Actions 运行记录，打开红色失败步骤，把日志复制出来，再发给 AI 分析。
