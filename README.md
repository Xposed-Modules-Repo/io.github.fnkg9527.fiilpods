<div align="center">

# FiilPods

**让 FIIL 耳机接入小米 HyperOS 的系统耳机体验**

[![Android 15+](https://img.shields.io/badge/Android-15%2B-3DDC84?style=flat-square&logo=android&logoColor=white)](https://www.android.com/)
[![HyperOS](https://img.shields.io/badge/ROM-HyperOS-FF6900?style=flat-square)](https://hyperos.mi.com/)
[![LSPosed](https://img.shields.io/badge/Framework-LSPosed-6F42C1?style=flat-square)](https://github.com/LSPosed/LSPosed)
[![License](https://img.shields.io/github/license/FNKG9527/FiilPods?style=flat-square)](https://github.com/FNKG9527/FiilPods/blob/main/LICENSE)

</div>

---

## 这是什么

小米 HyperOS 只对自家耳机开放那套「原生耳机体验」——下拉控制中心的融合设备卡片、系统蓝牙详情页、超级岛、佩戴检测、系统级降噪切换。FIIL 耳机插上来只被当成一只普通蓝牙耳机。

FiilPods 是一个 LSPosed 模块，注入系统蓝牙进程，直接讲 FIIL 自己的私有协议（经典蓝牙 SPP / RFCOMM 与 BLE GATT），再把结果翻译成 MIUI/HyperOS 认识的形式。装上之后，FIIL 耳机在系统里长得就像一只小米耳机。

模块不弹自己的悬浮窗、不常驻前台、不接管通知栏——所有界面都是系统原生的。

## 功能

| 能力 | 说明 |
| --- | --- |
| 融合设备中心 | 下拉控制中心的耳机卡片，降噪/通透切换与图标实时刷新 |
| 系统蓝牙详情页 | 电量、固件、型号、降噪、EQ、空间音频、LDAC 开关 |
| 焦点通知 / 超级岛 | 连接与电量变化的原生提示 |
| 佩戴检测 | 摘下暂停、戴回播放 |
| 降噪读写 | 系统级 ANC 接口直接落到 FIIL 的协议命令上 |
| LDAC | 补上了官方 App 里那个「耳机侧开关」，并回读解锁状态 |
| 型号识别 | 按 earType 显示对应型号的官方产品图；头戴式与入耳式在融合中心用不同图标 |
| 设备身份 | 可伪装成受支持的型号，让系统放开本会隐藏的开关 |

## 支持设备

FIIL 全线真无线与头戴耳机（按 earType 识别），已验证 FIIL Key Max（头戴式，走 RFCOMM MATE 协议）。协议族分 GAIA 与 Mate 两支，模块按机型自动分流。

其他品牌的耳机不在支持范围内；同作者的 HuaweiPods / HyperPods 分别覆盖华为与 AirPods。

## 安装

1. 需要 LSPosed（或兼容的 libxposed API 102 框架）。
2. 安装本模块，在 LSPosed 里**启用**，作用域勾选：
   `com.android.bluetooth`、`com.xiaomi.bluetooth`、`com.milink.service`、`com.android.settings`
3. **装完或改完作用域后，关开一次蓝牙**（或重启手机）——LSPosed 只在进程启动时注入，不重启蓝牙进程 hook 不会生效。
4. 连接 FIIL 耳机，打开模块 App 确认连接状态。

## 已知限制

- 状态栏小图标仍是系统默认的蓝牙图标：官方型号图是不透明彩色产品照，Android 状态栏只取 alpha 单色着色，压成剪影后认不出型号。
- LDAC 需要耳机侧先解锁高清音频（FIIL+ 官方 App 里的那一步），未解锁时详情页会提示。
- 机型识别依赖 earType；遇到未收录的新型号可以在设置里手动指定。

## 相关链接

- 源码与问题反馈：<https://github.com/FNKG9527/FiilPods>
- 更新日志：<https://github.com/FNKG9527/FiilPods/blob/main/CHANGELOG.md>
- 第三方许可：[THIRD_PARTY_LICENSES.md](https://github.com/FNKG9527/FiilPods/blob/main/THIRD_PARTY_LICENSES.md)

## 致谢

本项目的界面与工程骨架来自 [OppoPods](https://github.com/1812z/OppoPods)，Hook 基础设施参考 [HuaweiPods](https://github.com/Nshpiter/HuaweiPods)，超级岛形态参考 [HyperPods](https://github.com/Art-Chen/HyperPods)。协议事实来自对 FIIL+ 官方 App 与 MiLink 系统组件的逆向分析。

本项目以 GPL-3.0 发布。
