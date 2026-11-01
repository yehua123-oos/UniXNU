# NativePrelink

Kernel prelink emitter and tooling. Binds the native kernel to the original kexts and writes the prelink plan.

| Repository | Maintainer | Scope |
| --- | --- | --- |
| [NativePrelink](https://github.com/UniXNU/NativePrelink) | [UniXNU](https://github.com/UniXNU) | Kernel prelink emitter and tooling. Binds the native kernel to the original kexts and writes the prelink plan. |

## State

Used by every kernel build. The ABI must match the pinned kernelcache.

## Build

Linked into XNU by `unixnu build kernel`, or built by its own script when the repository is a kit or tool.
