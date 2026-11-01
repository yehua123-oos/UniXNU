# NativeMobileDisplay

移动显示驱动和 GPU scanout 交接。校验 swap、回收帧并驱动固件 framebuffer。

| 仓库 | 维护者 | 范围 |
| --- | --- | --- |
| [NativeMobileDisplay](https://github.com/UniXNU/NativeMobileDisplay) | [UniXNU](https://github.com/UniXNU) | 移动显示驱动和 GPU scanout 交接。校验 swap、回收帧并驱动固件 framebuffer。 |

## 状态

CPU 和 GPU scanout 路径工作。GOP scanout 没有 vblank 中断；`sheng-vsync` 提供定时器。

## 构建

通过 `unixnu build kernel` 链接进 XNU；kit 或工具仓库用自己的脚本构建。
