# NativeUfs

Native UFS storage driver. Owns the host controller, SMMU, queues and the root read path.

| Repository | Maintainer | Scope |
| --- | --- | --- |
| [NativeUfs](https://github.com/UniXNU/NativeUfs) | [UniXNU](https://github.com/UniXNU) | Native UFS storage driver. Owns the host controller, SMMU, queues and the root read path. |

## State

The native UFS root works on sheng. SM8550 and SM7325 register paths are supported.

## Build

Linked into XNU by `unixnu build kernel`, or built by its own script when the repository is a kit or tool.
