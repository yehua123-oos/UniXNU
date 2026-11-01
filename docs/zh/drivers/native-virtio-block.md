# NativeVirtioBlock

Virtio 块驱动。向 XNU 发布 virtio 磁盘，可选用 verified root 路径。

| 仓库 | 维护者 | 范围 |
| --- | --- | --- |
| [NativeVirtioBlock](https://github.com/UniXNU/NativeVirtioBlock) | [UniXNU](https://github.com/UniXNU) | Virtio 块驱动。向 XNU 发布 virtio 磁盘，可选用 verified root 路径。 |

## 状态

QEMU 和 DroidVM 使用它。QEMU 移植已到 iPadOS 主屏幕。

## 构建

通过 `unixnu build kernel` 链接进 XNU；kit 或工具仓库用自己的脚本构建。
