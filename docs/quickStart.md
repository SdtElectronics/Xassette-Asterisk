# Quick Start
## Burn Tina Firmware
Get the firmware in [releases](https://github.com/SdtElectronics/Xassette-Asterisk/releases/tag/fw-v0.1-beta). Extract the tarball and you will get a card image. It could be burned to a SD using `dd` command:
```bash
dd if=fw.bin of=${card} bs=512
```
where ${card} is the path to the device file (under `/dev/`) to your card.

## Access The Shell via ADB
The firmware is preconfigured so that it works as an ADB USB gadget after booted up. Connect the board via the otg port and if your computer has installed ADB and corresponding drivers, the shell should be prompted after entering
```bash
adb shell
```

## Debugging via Serial
The serial prints boot log and kernel messages in addition to the shell prompt. The default debug serial is `UART0` at `PE3` and `PE2`. It can be easily connected with a pinheader at the bottom right of the board.