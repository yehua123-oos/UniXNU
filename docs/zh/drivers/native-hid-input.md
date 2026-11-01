# NativeHidInput

HID 输入驱动。通过原始 IOHID 栈发布触控和硬件按键。

| 仓库 | 维护者 | 范围 |
| --- | --- | --- |
| [NativeHidInput](https://github.com/UniXNU/NativeHidInput) | [UniXNU](https://github.com/UniXNU) | HID 输入驱动。通过原始 IOHID 栈发布触控和硬件按键。 |

## 状态

sheng 和多个设备移植使用它。驱动没有独立的真机结果。

## 构建

通过 `unixnu build kernel` 链接进 XNU；kit 或工具仓库用自己的脚本构建。
