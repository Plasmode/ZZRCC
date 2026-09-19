# ZZRCC Interface to 128x128 gray scale OLED display
### Introduction
128×128 gray scale OLED based on [SSD1327](https://github.com/Plasmode/ZZRCC/blob/main/Projects/ssd1327_v1.8.pdf) is now (2021) inexpensive and readily available. This page describes the hardware and software interface to such display and provides several example programs.

![greyscale](zzrcc_rev0_i2c_grey_scale.jpg)

### Hardware Interface
The 128×128 OLED display based on SSD1327 has an I2C interface, but the pin assignments are not compatible with ZZRCC (rev0 pc borad) assignment. The ZZRCC's I2C pin assignments are **SDA SCL GND VCC**, while 128×128 OLED display pin assignments are **SDA SCL VCC GND**. An adapter that switches the power and ground pins are required to connect the 128×128 OLED display to ZZRCC's I2C connector.

### Software Interface
Here are several example programs for driving the 128×128 display.

