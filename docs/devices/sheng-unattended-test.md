# Unattended test cycle

Two boot arguments make a sheng hardware run unattended. Neither is enabled by default.

| Argument | Effect |
| --- | --- |
| `sheng-log=1` | Starts `BootLog` from the board monitor. It writes the diagnostic page, banner, GPU rows and kernel message buffer to the last 32 MiB of `userdata`. |
| `sheng-autoreset=<seconds>` | After that many seconds of log time, writes the PMIC reboot-reason cell and resets into fastboot. It runs only with `sheng-log=1`. |

Build the test image with both arguments:

```sh
./unixnu build payload --unique-chip-id <hex> --trust-cache <bundle> --data-ramdisk <seed> \
  --kernel-arg=sheng-log=1 --kernel-arg=sheng-autoreset=120
```

The log writer opens the window only after NativeUfs has read the root layout. The reset happens once, after that round's log is on the medium.

## Log reader

The reader is a fastboot-boot-only Linux image. It copies the log window into RAM, offers a USB CDC ACM shell and mounts nothing. Build it from the pinned Linux release inputs:

```sh
python3 package/linux-log/build-linux-log-boot.py \
  --boot boot_sheng_singleboot.img --busybox busybox \
  --rebootbl rebootbl --module nvmem-reboot-mode.ko \
  --out out/sheng/boot/sheng-linux-log.img
```

`rebootbl` is the static aarch64 Linux program in `package/linux-log/rebootbl.cpp`. It calls `reboot(RESTART2, "bootloader")` through the device tree's `nvmem-reboot-mode` cell.

## Run

```sh
fastboot boot out/sheng/boot/boot.img
# Wait for the tablet to return to fastboot by itself.
fastboot boot out/sheng/boot/sheng-linux-log.img
python3 scripts/read-sheng-log.py --wait 240
```

`read-sheng-log.py` fetches the window over `/dev/cu.usbmodem*`, writes `build/sheng-logs/<tag>-<boot id>/` and then runs `rebootbl`. The tablet returns to fastboot for the next image.

The one-command form runs the same cycle:

```sh
SERIAL=<serial> READER=out/sheng/boot/sheng-linux-log.img \
  scripts/run-sheng-unattended.sh out/sheng/boot/boot.img 420
```

If the tablet does not return within the limit, the script says so and waits for a manual fastboot entry.

## Default off

- `board.toml` and the default kernel arguments do not set `sheng-log` or `sheng-autoreset`.
- `BootLog.c` and `BootReset.c` are compiled into the kernel, but they do nothing without those arguments.
- The build scripts do not add the arguments to any image.

## Offline check

`package/linux-log/check-linux-log-qemu.py` boots the reader in QEMU virt with a GPT disk that holds a synthetic log window. It checks partition lookup, the copy, the transfer and the decoder. It does not cover USB, UFS or the XNU writer.
