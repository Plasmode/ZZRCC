# Getting Started with ZZRCC
### Introduction
This guide starts off with an assembled ZZRCC and go through the procedure of power it up and install new compact flash disk

![annotated](..ZZRCC_rev0_annotated_topview.jpg)

Power
ZZRCC requires 5V, 250mA power source with a 2.1mm X 5.5mm power plug. Be sure the center lead is 5V and the barrel is ground.

Serial Port
ZZRCC is designed to communicate with 6-pin CP2102 USB-to-serial as shown in the picture below. Pin 1 of 6-pin CP2102 is DTR which is an output from CP2102 that conflicts with the RTS output of ZZRCC. The RTS handshake is not needed in current setup. The easiest way of resolving the conflict is not populate R5, 100 ohm resistor. Another method is to cut the trace on CP2102 adapter.
