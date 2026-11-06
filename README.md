# AmooBuddy

> **暂不开源，不建议逆向。**

装在 Android 手机上的本机执行桥。它把手机能力交给可信 Agent（例如手机主屏左滑的 Amoo），Agent 通过手机本机的 HTTP、文件信箱或 MCP 通道下发操作。

## 功能

- 读取控件树与截图，在其他 App 内点击、填字、滚动、返回。
- 执行 shell 命令、读写文件、启动应用、读取电量与剪贴板。
- 会话、租约、暂停、风险词确认和快照校验管住每一步。
- 可选：硬件触控外设、虚拟后台屏、视觉规划器、SKILL 经验库。
- 发布包带防重打包自检；签名不符时销毁本机凭据。

不提供 root，不绕过锁屏，不承诺任意 App 可用。

## 版本

遵循 [SemVer 2.0](https://semver.org/lang/zh-CN/)：`主版本.次版本.修订版本`，预发布用 `-rc.N`，构建元数据用 `+build.N`。

- Git 标签：`vX.Y.Z`
- 安装包：`amoobuddy-X.Y.Z.apk`
- Android `versionCode` 只要求单调递增，不参与 SemVer。

当前版本 **1.8.0**（由 `1.8.0-candidate.4` 毕业，versionCode 88）。

## 下载与校验

从本仓库的 Releases 下载 `amoobuddy-1.8.0.apk`。`main` 分支里无版本号的 `stepx-amoo-bridge-release.apk` 是历史包，已废弃。

```bash
apksigner verify --print-certs amoobuddy-1.8.0.apk
adb install amoobuddy-1.8.0.apk
```

签名 SHA-256 必须与 Release 说明一致。覆盖安装需要同一签名。

发布包做了 R8 混淆、资源收缩与签名。混淆只提高读码成本，不提供保密。守卫在发布构建生效，检测签名不符、调试、注入与可疑环境时销毁本机令牌，不改系统设置、不删用户数据。

## 上游与致谢

- 致敬原始 [amoobridge](https://github.com/luckybeet/amoobridge)。本项目在其思路上继续开发，上游仓库保留为 `upstream`。
- 参考了 Mika（`io.github.ccch1mneyyy.dsh_app`）的无障碍悬浮层与虚拟屏预览交互，用于后台小窗与遮挡判定。
- 另吸收 Andee、Neo Agent Touch、GELab-Zero 等公开研究的观察与操作闭环思路。

公开仓库只提供已签名的安装包与说明，源码暂不公开。
