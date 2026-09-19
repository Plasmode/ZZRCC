# Testing ZZRCC without CF disk
The following is the procedure for booting ZZRCC without CF disk:

1. Download and unzip ZZRCC serial loader and ZZRCC monitor from software section of ZZRCC homepage,
2. Remove the jumper across T10-T11 (T10 and T11 are right next to the 2.1mm X 5.5mm power jack)
3. Power up ZZRCC, the current draw is 180mA nominally without CF disk.
4. Set serial port to 115200, odd parity, 8 data bit and 1 stop bit
5. Check the “Binary” box of TeraTerm Send file menu and send ZRSERLDR.BIN to ZZRCC. You should see the sign on message:

```
ZZRCC Loader v0.1
Change serial port to 115200 N81
Auto start at 0xB400
```
6. Change serial port setting to 115200, no parity, 8 data bit, 1 parity bit
7. Un-check the “Binary” box of TeraTerm Send file menu and send ZZRMon.hex to ZZRCC, you should see the message:
```
…………………………………………………………………………………………………………………………………………………………………………………………………….UX
ZZRCC Monitor v0.5 4/16/21
```
8. ZZRCC monitor is now running. 'h' will list the monitor commands. 't' will test RAM. Do not run commands associated with CF disk (R,X,B,C) because it will hang.
