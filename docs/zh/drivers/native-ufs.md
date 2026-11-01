# NativeUfs

原生 UFS 存储驱动。负责主机控制器、SMMU、队列和根卷读取路径。

| 仓库 | 维护者 | 范围 |
| --- | --- | --- |
| [NativeUfs](https://github.com/UniXNU/NativeUfs) | [UniXNU](https://github.com/UniXNU) | 原生 UFS 存储驱动。负责主机控制器、SMMU、队列和根卷读取路径。 |

## 状态

原生 UFS 根卷在 sheng 上工作。支持 SM8550 和 SM7325 寄存器路径。

## 构建

通过 `unixnu build kernel` 链接进 XNU；kit 或工具仓库用自己的脚本构建。
