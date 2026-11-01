# NativeMetal

Metal API 前端。通过 `MTLAddDevice` 发布 Metal 设备，用 metal2vulkan 翻译 AIR，再经 Turnip 和 NativeAdreno 提交。

| 仓库 | 维护者 | 范围 |
| --- | --- | --- |
| [NativeMetal](https://github.com/UniXNU/NativeMetal) | [UniXNU](https://github.com/UniXNU) | Metal API 前端。通过 `MTLAddDevice` 发布 Metal 设备，用 metal2vulkan 翻译 AIR，再经 Turnip 和 NativeAdreno 提交。 |

## 状态

sheng 上 GPU 合成的桌面已运行。首次 shader 编译较慢，没有完整的预编译 UI 包。

## 构建

通过 `unixnu build kernel` 链接进 XNU；kit 或工具仓库用自己的脚本构建。
