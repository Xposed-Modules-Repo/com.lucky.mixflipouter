<div align="center">

# WidgetEnhancer

**为 Xiaomi MIX Flip 外屏提供自定义小部件能力的 LSPosed 模块**

[![Release](https://img.shields.io/github/v/release/Xposed-Modules-Repo/com.lucky.mixflipouter?label=Release)](https://github.com/Xposed-Modules-Repo/com.lucky.mixflipouter/releases/latest)
[![License](https://img.shields.io/badge/License-GPL--3.0--only-blue.svg)](https://github.com/luckylca/WidgetEnhancer/blob/main/LICENSE)
[![Source](https://img.shields.io/badge/Source-WidgetEnhancer-black)](https://github.com/luckylca/WidgetEnhancer)

</div>

WidgetEnhancer 将自定义小部件直接接入 HyperOS 原生外屏小部件系统。创建后的小部件会出现在「设置 → 外屏 → 小部件 → 自定义」中，可以和官方小部件一样添加、删除、排序和使用。

> **兼容性**：当前主要适配 Xiaomi MIX Flip（`ruyi`），需要 Root、LSPosed 和 HyperOS 外屏桌面 `com.miui.fliphome`。

## 功能

### 媒体小部件

- 支持图片和循环视频
- 支持裁剪、缩放和位置调整
- 按照外屏比例生成预览
- 视频支持循环播放

### 音乐小部件

- 显示歌曲名称、歌手和专辑封面
- 显示当前歌词与下一句歌词
- 支持 MediaSession 播放状态与媒体控制
- 支持网易云音乐同步歌词适配

| 操作 | 功能 |
| --- | --- |
| 单击 | 播放 / 暂停 |
| 双击上半区域 | 上一首 |
| 双击下半区域 | 下一首 |
| 长按上半区域 | 增加音量 |
| 长按下半区域 | 降低音量 |

### 快捷按钮小部件

可以创建包含 **1～6 个按钮**的快捷小部件，并根据按钮数量自动匹配布局。

支持绑定应用和常用系统操作，包括：

- 打开应用
- 音量控制与静音
- 手电筒
- 勿扰模式
- 自动旋转
- 锁屏
- 播放 / 暂停、上一首、下一首
- 部分快捷设置功能

## 小部件管理

模块自带配置应用，可用于创建、编辑、删除、重命名、预览和导入小部件。

创建完成后进入：

```text
设置
→ 外屏
→ 小部件
→ 自定义
```

即可将自定义小部件添加到外屏。

## 实现原理

WidgetEnhancer 基于 LSPosed / Xposed Hook 实现，主要作用于：

```text
com.miui.fliphome
```

模块将自定义小部件信息注入 HyperOS 原有的小部件列表，并尽可能继续使用系统原有的添加、删除、排序、页面管理和持久化逻辑。

```text
WidgetEnhancer
      │
      ├── 小部件配置与数据
      │
      └── LSPosed Hook
               │
               ▼
        com.miui.fliphome
               │
               ├── 官方小部件列表
               ├── 添加 / 删除 / 排序
               └── 外屏页面
                       │
                       ▼
                自定义小部件
```

因此模块主要负责自定义小部件的配置、数据和显示内容，而不是重新实现一套独立的外屏桌面。

## LSPosed 作用域

### 必选

```text
com.miui.fliphome
```

### 可选：网易云音乐

```text
com.netease.cloudmusic
```

用于启用更完整的网易云音乐同步歌词适配。

### 可选：SystemUI

```text
com.android.systemui
```

用于部分高级快捷设置功能。

## 安装

1. 下载并安装最新版本 APK。
2. 在 LSPosed 中启用 WidgetEnhancer。
3. 至少勾选 `com.miui.fliphome` 作用域。
4. 根据需要勾选网易云音乐或 SystemUI 可选作用域。
5. 重启手机。
6. 打开 WidgetEnhancer 创建小部件，并在系统外屏设置中添加。

## 权限

根据所使用的功能，可能需要授予：

- 通知使用权：获取媒体播放状态和音乐信息
- 相机权限：控制手电筒
- 勿扰模式访问权限：控制勿扰模式
- 修改系统设置权限：控制自动旋转等功能

不使用对应功能时无需授予相关权限。

## 源代码

源码、问题反馈与开发信息：

https://github.com/luckylca/WidgetEnhancer

## 开源协议

WidgetEnhancer 采用 **GNU General Public License v3.0 only（GPL-3.0-only）** 开源。

许可证内容：

https://github.com/luckylca/WidgetEnhancer/blob/main/LICENSE
