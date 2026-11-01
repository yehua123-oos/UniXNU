# NativeMobileDisplay

Mobile display driver and GPU scanout hand-off. Validates swaps, retires frames and drives the firmware framebuffer.

| Repository | Maintainer | Scope |
| --- | --- | --- |
| [NativeMobileDisplay](https://github.com/UniXNU/NativeMobileDisplay) | [UniXNU](https://github.com/UniXNU) | Mobile display driver and GPU scanout hand-off. Validates swaps, retires frames and drives the firmware framebuffer. |

## State

The CPU and GPU scanout paths work. The GOP scanout has no vblank interrupt; `sheng-vsync` supplies a timer.

## Build

Linked into XNU by `unixnu build kernel`, or built by its own script when the repository is a kit or tool.
