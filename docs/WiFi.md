# WiFi
Xassette-Asterisk supports SDIO Wi-Fi module since hw v0.2. The module is connected to SoC via `sdc2` which shares pins with SPI flash, thus the flash won't be available when Wi-Fi module is in use.

## Module Selection
Due to the limited area of PCB, there is no onboard antenna for the module. Thus the module must have an IPEX socket to connect external antenna. RTL8189ftv is the module used to test the Wi-Fi functionality, and it will be the example for the following sections.

## Kernel Configuration
To enable the `sdc2` interface as SDIO card controller, the board device tree must configure `sdc2` as below:
```c
&sdc2 {
        non-removable;
        bus-width = <4>;
        no-mmc;
        no-sd;
        cap-sd-highspeed;
        cap-sdio-irq;
        keep-power-in-suspend;
        ignore-pm-notify;
        max-frequency = <150000000>;
        ctl-spec-caps = <0x308>;
        status = "okay";
};
```
and the `no-sdio` property must be removed from the `sdc2` node in chip's device tree (sun20iw1p1.dtsi).

After this, the SD card will probably be probed as `mmcblk1` (originally `mmcblk0`) and causes the VFS fail to mount the root partition. Changing the path of root (in bootargs) in u-boot solves the problem.

The firmware image with configuration supports Wi-Fi is available in [release](https://github.com/SdtElectronics/Xassette-Asterisk/releases/tag/fw-v0.2). It can be flashed to the card following [Quick Start](docs/quickStart.md).

## Driver
Driver for RTL8189ftv can be compiled following [sunxi WiKi](https://linux-sunxi.org/Wifi#RTL8189FTV). This driver is included in the firmware mentioned above. Load it with 
```
insmod 8189fs
```
and the module is ready to work.