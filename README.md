# 掌卦 v0.1

这是掌卦 v0.1 的公开发布仓库，只包含发布说明和可刷写固件。源码和开发记录保留在私有仓库。

## 分支

当前公开分支：`release/0.1`

## 支持硬件

| 硬件 | 固件目录 | 芯片 | 说明 |
| --- | --- | --- | --- |
| M5Stack StickS3 | `firmware/m5stack-sticks3` | `esp32s3` | 已上机检查 |
| M5Stack StickC Plus | `firmware/m5stack-stickc-plus` | `esp32` | 已通过编译，仍需真机检查 |
| M5Stack StickC Plus2 | `firmware/m5stack-stickc-plus2` | `esp32` | 已通过编译，仍需真机检查 |

## 文件

每个固件目录包含：

- `bootloader.bin`
- `partitions.bin`
- `boot_app0.bin`
- `firmware.bin`

`SHA256SUMS.txt` 记录所有二进制文件的 SHA-256。

## 校验

```sh
shasum -a 256 -c SHA256SUMS.txt
```

## 刷写

先安装 `esptool`：

```sh
python3 -m pip install esptool
```

把下面命令里的 `PORT` 改为实际串口，例如 `/dev/cu.usbmodem21201` 或 `/dev/cu.usbserial-0001`。

### M5Stack StickS3

```sh
python3 -m esptool --chip esp32s3 --port PORT --baud 1500000 --before default_reset --after hard_reset write_flash -z --flash_mode dio --flash_freq 80m --flash_size 8MB \
  0x0000 firmware/m5stack-sticks3/bootloader.bin \
  0x8000 firmware/m5stack-sticks3/partitions.bin \
  0xe000 firmware/m5stack-sticks3/boot_app0.bin \
  0x10000 firmware/m5stack-sticks3/firmware.bin
```

### M5Stack StickC Plus

```sh
python3 -m esptool --chip esp32 --port PORT --baud 1500000 --before default_reset --after hard_reset write_flash -z --flash_mode dio --flash_freq 40m --flash_size 4MB \
  0x1000 firmware/m5stack-stickc-plus/bootloader.bin \
  0x8000 firmware/m5stack-stickc-plus/partitions.bin \
  0xe000 firmware/m5stack-stickc-plus/boot_app0.bin \
  0x10000 firmware/m5stack-stickc-plus/firmware.bin
```

### M5Stack StickC Plus2

```sh
python3 -m esptool --chip esp32 --port PORT --baud 1500000 --before default_reset --after hard_reset write_flash -z --flash_mode dio --flash_freq 40m --flash_size 4MB \
  0x1000 firmware/m5stack-stickc-plus2/bootloader.bin \
  0x8000 firmware/m5stack-stickc-plus2/partitions.bin \
  0xe000 firmware/m5stack-stickc-plus2/boot_app0.bin \
  0x10000 firmware/m5stack-stickc-plus2/firmware.bin
```
