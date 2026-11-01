# NativeMetal

Metal API frontend. Publishes a Metal device through `MTLAddDevice`, translates AIR with metal2vulkan and submits through Turnip and NativeAdreno.

| Repository | Maintainer | Scope |
| --- | --- | --- |
| [NativeMetal](https://github.com/UniXNU/NativeMetal) | [UniXNU](https://github.com/UniXNU) | Metal API frontend. Publishes a Metal device through `MTLAddDevice`, translates AIR with metal2vulkan and submits through Turnip and NativeAdreno. |

## State

The GPU-composited desktop runs on sheng. First-use shader compilation is slow and there is no complete precompiled UI pack.

## Build

Linked into XNU by `unixnu build kernel`, or built by its own script when the repository is a kit or tool.
