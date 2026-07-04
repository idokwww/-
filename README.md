# Ace6 iPhone Spoof

基于 LSPosed/Xposed 的上层机型信息 Hook 示例模块，面向一加 Ace6、Magisk、KernelSU + Zygisk/LSPosed 环境。

## 功能

- Hook `android.os.Build` 常用字段：
  - `Build.MODEL`
  - `Build.BRAND`
  - `Build.MANUFACTURER`
  - `Build.FINGERPRINT`
  - `Build.PRODUCT`
  - `Build.DEVICE`
  - `Build.BOARD`
  - `Build.HARDWARE`
- Hook `Build.VERSION` 部分字段：
  - `RELEASE`
  - `INCREMENTAL`
  - `SECURITY_PATCH`
  - `BASE_OS`
- Hook `android.os.SystemProperties`：
  - `get(String)`
  - `get(String, String)`
  - `getInt`
  - `getLong`
  - `getBoolean`
- Hook 部分 Java 层 `ProcessBuilder.start()` 和 `Runtime.exec()` 调用的 `getprop` 命令。

## 伪装目标

```text
brand: Apple
manufacturer: Apple
model: iPhone 17 Pro
product: iPhone17Pro
device: iPhone17,1
hardware: A19Pro
fingerprint: Apple/iPhone17Pro/iPhone17,1:18.0/22A3354/22A3354:user/release-keys
```

## 编译 APK

1. 使用 Android Studio 打开本项目。
2. 等待 Gradle Sync 完成。
3. 执行：

```bash
./gradlew assembleDebug
```

生成文件：

```text
app/build/outputs/apk/debug/app-debug.apk
```

也可以在 Android Studio 中选择 `Build > Build Bundle(s) / APK(s) > Build APK(s)`。

## LSPosed 使用教程

1. 确认设备已经安装并启用 Magisk 或 KernelSU。
2. 安装 Zygisk LSPosed。
3. 安装本项目编译出的 APK。
4. 打开 LSPosed。
5. 在“模块”中启用 `Ace6 iPhone Spoof`。
6. 在“作用域”中选择需要伪装的目标应用。
7. 强制停止目标应用，重新打开。
8. 禁用模块或移除作用域后，重新启动目标应用即可恢复原始读取结果。

## 开关说明

本模块没有修改 system 分区，也不写系统属性文件。所谓启用/禁用由 LSPosed 模块开关和作用域控制：

- 启用模块并选择目标应用后，目标应用新进程内读取到伪装信息。
- 禁用模块或移除目标应用作用域后，目标应用新进程会恢复读取系统原始信息。
- 已经运行中的应用需要强制停止后重新打开。

## 安全与残留

本模块不修改 system 分区，不修改 boot/vendor，不写入系统属性文件，不修改内核。所有伪装仅在被 LSPosed 注入的应用进程中生效。

## 限制

本模块只能 Hook 上层 Java API。

无法修改或稳定伪装：

- Linux 内核标识
- CPU 架构
- 硬件节点
- `/proc`、`/sys` 文件
- native 层直接读取
- TEE、KeyStore、安全芯片返回值
- SafetyNet、Play Integrity、厂商风控、游戏反作弊、安全校验接口

`getprop` 是系统二进制命令，模块只能拦截部分 Java 层启动 `getprop` 的调用。native 直接调用、shell 环境、系统服务真实属性值不会被真正修改。

## 免责声明

代码仅限安卓逆向技术学习研究，严禁用于绕过风控、游戏作弊、违规用途。请遵守法律法规。
