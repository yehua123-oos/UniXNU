# 无人值守测试流程

两个启动参数让 sheng 的硬件测试无人值守。两者默认都不开启。

| 参数 | 作用 |
| --- | --- |
| `sheng-log=1` | 从板级监控启动 `BootLog`，把诊断页、banner、GPU 行和内核消息缓冲写入 `userdata` 最后 32 MiB。 |
| `sheng-autoreset=<秒>` | 日志时间达到该秒数后，写入 PMIC reboot-reason cell 并重启到 fastboot。只在 `sheng-log=1` 时运行。 |

构建同时带两个参数的测试镜像：

```sh
./unixnu build payload --unique-chip-id <hex> --trust-cache <bundle> --data-ramdisk <seed> \
  --kernel-arg=sheng-log=1 --kernel-arg=sheng-autoreset=120
```

日志写入器在 NativeUfs 读取根布局后才打开窗口。reset 只执行一次，且在该轮日志落盘之后。

## 日志读取器

读取器是只通过 fastboot 启动的 Linux 镜像。它把日志窗口复制到 RAM，提供 USB CDC ACM shell，不挂载任何分区。用固定的 Linux release 输入构建：

```sh
python3 package/linux-log/build-linux-log-boot.py \
  --boot boot_sheng_singleboot.img --busybox busybox \
  --rebootbl rebootbl --module nvmem-reboot-mode.ko \
  --out out/sheng/boot/sheng-linux-log.img
```

`rebootbl` 是 `package/linux-log/rebootbl.cpp` 中的静态 aarch64 Linux 程序。它通过设备树的 `nvmem-reboot-mode` cell 调用 `reboot(RESTART2, "bootloader")`。

## 运行

```sh
fastboot boot out/sheng/boot/boot.img
# 等待平板自行回到 fastboot。
fastboot boot out/sheng/boot/sheng-linux-log.img
python3 scripts/read-sheng-log.py --wait 240
```

`read-sheng-log.py` 通过 `/dev/cu.usbmodem*` 取回窗口，写入 `build/sheng-logs/<tag>-<boot id>/`，然后运行 `rebootbl`。平板回到 fastboot，可以启动下一个镜像。

一条命令跑完整轮：

```sh
SERIAL=<serial> READER=out/sheng/boot/sheng-linux-log.img \
  scripts/run-sheng-unattended.sh out/sheng/boot/boot.img 420
```

如果平板没有在时限内返回，脚本会提示并等待手动进入 fastboot。

## 默认关闭

- `board.toml` 和默认内核参数不设置 `sheng-log` 或 `sheng-autoreset`。
- `BootLog.c` 和 `BootReset.c` 会编译进内核，但没有上述参数时不执行。
- 构建脚本不会把参数加入任何镜像。

## 离线检查

`package/linux-log/check-linux-log-qemu.py` 在 QEMU virt 中启动读取器，使用带合成日志窗口的 GPT 磁盘，检查分区查找、复制、传输和解码。它不覆盖 USB、UFS 或 XNU 写入器。
