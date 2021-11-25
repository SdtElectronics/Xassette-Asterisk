# Troubleshooting

## General
Check voltages of each group of power. The typical voltages for power nets are:
- `3V3`: 3.3V
- `1V8`: 1.8V
- `VDD-CORE`: 0.9V
- `LDOB-OUT`: 1.2-1.3V in FEL mode, 1.8V in normal operation

Check whether there are bad electrical connections.

Check whether separate nets are accidently connected.

## Nothing Is Printed to Serial
Check whether TX and RX signals are matched. Try interchanging them. Remove the boot media and connect the board to a computer via the otg port. If a new device is detected by the computer, it means the chip worked properly and you should check the boot media. Otherwise use an oscilloscope to check whether the crystal is oscillating. If not, check the power, and in worst cases the chip is probably dead.

## System Frequently Hangs or Reboot
Use a better power supply. Remove the load capacitors of 24M crystal (`C13`, `C14`). If the problem is eliminated it indicates the value of load capacitors was too large.

## MMC Errors or Reboot after Mounting New Partion
Check the soldering of the card slot. Use a better card as bad blocks can cause failure.

## LCD Is Not Working
If the backlight is not up, check the boost circuit. Otherwise check the level of `DISP` signal. It should be pulled high for most panels i.e. `R32` should be soldered.