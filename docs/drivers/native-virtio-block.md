# NativeVirtioBlock

Virtio block driver. Publishes virtio disks to XNU and optionally uses the verified root path.

| Repository | Maintainer | Scope |
| --- | --- | --- |
| [NativeVirtioBlock](https://github.com/UniXNU/NativeVirtioBlock) | [UniXNU](https://github.com/UniXNU) | Virtio block driver. Publishes virtio disks to XNU and optionally uses the verified root path. |

## State

Used by QEMU and DroidVM. The QEMU port reaches the iPadOS home screen.

## Build

Linked into XNU by `unixnu build kernel`, or built by its own script when the repository is a kit or tool.
