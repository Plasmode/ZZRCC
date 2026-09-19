# ZZRCC I2C Interface
## Introduction
ZZRCC has a 4-pin I2C connector and a bit-bang register in CPLD that controls the I2C signals. The following is an introduction to using the I2C function.

## I2C Connector Definition
The pin assignments of the I2C connector from left-to-right are

–annotated picture here— SDA, SCL, GND VCC

## I2C Register in CPLD
- I/O address is 0x9E
- SDA is data bit 0, open collector with external 2.4K pull up resistor
- SCL is data bit 1, CMOS output, no external pull up resistor.
- Data bit 2 to 7 are don't care
- Both SDA and SCL are high at reset.

## I2C Bit Bang Example
## I2C Start command
```
i2cs:
; I2C START command
; SCL is D[1], SDA is D[0]
    ld a,3
    out (I2C),a    ;set SCL and SDA high
    nop
    nop
    ld a,2
    out (I2C),a    ;START
    nop
    nop
    nop
    nop
    ld a,0
    out (I2C),a    ;clock low
    ret
```
### I2C Stop Command
i2cp:
;I2C STOP command
; SCL is D[1], SDA is D[0]
    ld a,0
    out (I2C),a
    ld a,2
    out (I2C),a
    nop
    nop
    nop
    nop
;data goes high while clock high (STOP)
    ld a,3
    out (I2C),a
    ret
```
### Bit bang a byte of data to I2C bus
```
;pass data in regA
;SCL is D[1], SDA is D[0], other bits are don't care
;roll 8 bit data around through carry flag, take care of not alter carry flag
;with set/res instruction SCL can be wiggled without changing rest of the data
;slave acknowledge is not checked so no error message when slave is not present
    push bc
    ld b,8         ;8 passes for 8 bits
    rla            ;msb into carry
wi2cN1:
    rla            ;in first pass: msb into bit0 (SDA), carry in bit 1 (SCL)
    res 1,a        ;make sure clock is low
    out (I2C),a    ;change data while clock is low
    set 1,a        ;clock is high
    out (I2C),a
    nop
    res 1,a        ;clock is low
    out (I2C),a
    djnz wi2cN1
    ld a,1         ;slave acknowledge cycle
    out (I2C),a
    ld a,3
    out (I2C),a
    ld a,1         ;no checking of slave acknowledge
    out (I2C),a
    pop bc
    ret
```
