# NativePrelink

内核预链接发射器和工具。把原生内核绑定到原始 kext，并写出预链接方案。

| 仓库 | 维护者 | 范围 |
| --- | --- | --- |
| [NativePrelink](https://github.com/UniXNU/NativePrelink) | [UniXNU](https://github.com/UniXNU) | 内核预链接发射器和工具。把原生内核绑定到原始 kext，并写出预链接方案。 |

## 状态

每次内核构建使用它。ABI 必须匹配固定的 kernelcache。

## 构建

通过 `unixnu build kernel` 链接进 XNU；kit 或工具仓库用自己的脚本构建。
