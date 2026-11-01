# NativeAES

原生 AES 加速器驱动。把原始加速器类绑定到记录的 XNU ABI。

| 仓库 | 维护者 | 范围 |
| --- | --- | --- |
| [NativeAES](https://github.com/UniXNU/NativeAES) | [UniXNU](https://github.com/UniXNU) | 原生 AES 加速器驱动。把原始加速器类绑定到记录的 XNU ABI。 |

## 状态

板级启用对应静态库时链接进 XNU。没有独立真机结果。

## 构建

通过 `unixnu build kernel` 链接进 XNU；kit 或工具仓库用自己的脚本构建。
